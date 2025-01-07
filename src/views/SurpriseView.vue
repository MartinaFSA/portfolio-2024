<template>
    <section class="focus-in">
        <h1>Which celestial body do you like more?</h1>
        <div class="surprise_inputs">
            <div
                v-for="(item, index) in fields"
                :key="index"
                class="ctn-input-radio"
            >
                <label :for="item.value" class="radio-circle">
                    <input
                        type="radio"
                        name="planet"
                        :value="item.value"
                        @change="selectedOption(item.value)"
                    />
                    <span>
                    <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="h-3.5 w-3.5"
                        viewBox="0 0 16 16"
                        fill="currentColor"
                    >
                        <circle data-name="ellipse" cx="8" cy="8" r="8"></circle>
                    </svg>
                    </span>
                </label>
                <label class="input-label" :for="item.value"
                    @click="selectedOption(item.value)"
                >{{item.name}}</label>
            </div>
        </div>
    </section>
    <section>
        <canvas ref="canvas"></canvas>
    </section>
</template>

<script>
    import * as THREE from 'three';
    
    export default {
        name: 'Surprise',
        data() {
            return {
                selectedPlanet: 'moon',
                fields: [ 
                    {name: 'Moon', value: 'moon'},
                    {name: 'Mars', value: 'mars'},
                    {name: 'Jupiter', value: 'jupiter'},
                    {name: 'Sun', value: 'sun'},
                ]
            }
        },
        mounted() {
            this.initThree();
            this.selectedOption(this.selectedPlanet);
            window.addEventListener('mousemove', this.onMouseMove);
        },
        beforeDestroy() {
            window.removeEventListener('mousemove', this.onMouseMove);
        },
        methods: {
            selectedOption(planet) {
                this.selectedPlanet = planet;
                //when clicking label, radio should get checked
                const radios = document.getElementsByName('planet');
                for (let i = 0; i < radios.length; i++) {
                    if (radios[i].value === planet) {
                        radios[i].checked = true;
                        break;
                    }
                }
                this.updatePlanet();
            },
            initThree() {
                this.camera = new THREE.PerspectiveCamera(45, this.aspect, 0.1, 1500);
                this.scene = new THREE.Scene();
                this.renderer = new THREE.WebGLRenderer({ canvas: this.$refs.canvas });
                this.textureLoader = new THREE.TextureLoader();
                this.camera.position.z = 5;
                this.cameraAutoRotation = true;
                this.renderer.setSize(window.innerWidth, window.innerWidth);
                this.renderer.setClearColor( 0xffffff, 0);
                this.aspect = window.innerWidth / window.innerWidth;
                this.cameraRotation = 0;
                this.cameraRotationSpeed = 0.001;
                this.createSaturnPlanet();
                this.animate();
            },
            createSaturnPlanet() {
                const planetGeometry = new THREE.SphereGeometry(1, 32, 32);

                const planetTexture = this.textureLoader.load('/src/assets/img/' + this.selectedPlanet + '.jpg');
                const planetMaterial = new THREE.MeshBasicMaterial({ map: planetTexture });

                this.planet = new THREE.Mesh(planetGeometry, planetMaterial);
                this.scene.add(this.planet);
            },
            onMouseMove(event) {
                const rotationX = (event.clientX / window.innerWidth) * 2 - 1;
                const rotationY = (event.clientY / window.innerWidth) * 2 - 1;

                this.planet.rotation.x = rotationY;
                this.planet.rotation.y = rotationX;
            },
            animate() {
                requestAnimationFrame(this.animate.bind(this));
                this.renderer.render(this.scene, this.camera);
            },
            updatePlanet() {
                const planetGeometry = new THREE.SphereGeometry(1, 32, 32);

                this.planet.material.dispose();
                this.scene.remove( this.planet );

                const planetTexture = this.textureLoader.load('/src/assets/img/' + this.selectedPlanet + '.jpg');
                const planetMaterial = new THREE.MeshBasicMaterial({ map: planetTexture });

                this.planet = new THREE.Mesh(planetGeometry, planetMaterial);
                this.scene.add(this.planet);
            },
        }
    }
</script>

<style scoped>
    section {
        display: flex;
        align-items: center;
        flex-direction: column;
        color: var(--white);
    } section:first-of-type {
        height: 10vh;
    }
    section h1 {
        text-align: center;
        font-size: 3rem;
        margin-top: 4vw;
    }
    label {
        font-size: 1.5rem;
    }
    input {
        margin-left: 20px;
        margin-right: 5px;
    } canvas {
        margin-top: 50px;
        max-width: 90vh;
        max-height: 90vh;
    }
    .surprise_inputs {
        display: flex;
    }
    .ctn-input-radio {
        line-height: 1.5;
        display: flex;
        align-items: center;
    }
    .ctn-input-radio svg {
        display: block;
        height: 0.875rem;
        width: 0.875rem;
    }

    .ctn-input-radio label {
        cursor: pointer;
        margin-top: 1px;
        user-select: none;
    }
    .ctn-input-radio label.radio-circle {
        align-items: center;
        border: 0 solid white;
        box-sizing: border-box;
        cursor: pointer;
        display: flex;
        padding: 0.55rem;
        position: relative;
        scrollbar-width: thin !important;
    }

    .ctn-input-radio input[type='radio'] {
        border: 1.5px solid white;
        appearance: none;
        box-sizing: border-box;
        color: white;
        cursor: pointer;
        font-family: inherit;
        font-feature-settings: inherit;
        font-size: 100%;
        font-variation-settings: inherit;
        font-weight: inherit;
        height: 1.25rem;
        line-height: inherit;
        margin: 0;
        padding: 0;
        position: relative;
        scrollbar-width: thin !important;
        transition: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);
        width: 1.25rem;
    }

    .ctn-input-radio input[type='radio']:before {
        background-color: white;
        border: 0 solid white;
        box-sizing: border-box;
        content: '';
        display: block;
        height: 2.2rem;
        width: 2.2rem;
        left: 50%;
        opacity: 0;
        position: absolute;
        top: 50%;
        transform: translate(-50%, -50%);
        transition: opacity 0.15s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .ctn-input-radio input[type='radio']:checked ~ span {
        opacity: 1;
    }

    .ctn-input-radio input[type='radio']:hover:not(:disabled):before {
        opacity: 0.1;
    }

    .ctn-input-radio label.radio-circle span {
        border: 0 solid white;
        box-sizing: border-box;
        color: white;
        left: 50%;
        opacity: 0;
        pointer-events: none;
        position: absolute;
        scrollbar-width: thin !important;
        top: 50%;
        transform: matrix(1, 0, 0, 1, -7, -7);
        transition: opacity 0.15s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .ctn-input-radio label.radio-circle {
        border-radius: 5px;
    }
    .ctn-input-radio input[type='radio'] {
        border: 1px solid white;
        border-radius: 9999px;
    }
    .ctn-input-radio input[type='radio']:before {
        border-radius: 9999px;
    }
    .ctn-input-radio input[type='radio']:placeholder {
        color: white;
        opacity: 1;
    }
    .ctn-input-radio input[type='radio']:checked:before {
        background-color: white;
    }

</style>