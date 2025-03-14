<!DOCTYPE html>
<html lang="en">
<head>
    <title>FluidSim WebApp</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            height: 100vh;
            margin: 0;
        }
        #toolbar {
            width: 200px;
            background: #f0f0f0;
            padding: 10px;
        }
        #workspace {
            flex: 1;
            background: #ffffff;
            border-left: 1px solid #ccc;
            position: relative;
        }
        .component {
            width: 80px;
            height: 80px;
            background: lightblue;
            border: 2px solid #007bff;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: grab;
            position: absolute;
        }
    </style>
</head>
<body>

<div id="toolbar">
    <h3>Pneumatic Components</h3>
    <div class="component" draggable="true" data-type="cylinder">Cylinder</div>
    <div class="component" draggable="true" data-type="valve">5/2 Valve</div>
    <div class="component" draggable="true" data-type="air">Air Supply</div>
    <div class="component" draggable="true" data-type="button">Button</div>
    <div class="component" draggable="true" data-type="actuator">Actuator</div>
</div>

<div id="workspace"></div>

<script>
    const components = document.querySelectorAll('.component');
    const workspace = document.getElementById('workspace');

    components.forEach(component => {
        component.addEventListener('dragstart', (e) => {
            e.dataTransfer.setData('type', e.target.dataset.type);
        });
    });

    workspace.addEventListener('dragover', (e) => {
        e.preventDefault();
    });

    workspace.addEventListener('drop', (e) => {
        e.preventDefault();
        const type = e.dataTransfer.getData('type');

        const newComponent = document.createElement('div');
        newComponent.classList.add('component');
        newComponent.innerText = type;
        newComponent.style.left = `${e.clientX - workspace.offsetLeft - 40}px`;
        newComponent.style.top = `${e.clientY - workspace.offsetTop - 40}px`;

        newComponent.onclick = () => {
            alert(`AI Help: This is a ${type}. Click on the lightbulb for more information.`);
        };

        workspace.appendChild(newComponent);
    });
</script>

</body>
</html>
