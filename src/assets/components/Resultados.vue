<script>
import {
    obtenerPorcentaje,
    obtenerResultadosCalculos
} from "../../utils/calculos"
export default {
    props: {
        datosFormulario: Object
    },
    computed: {
        porcentaje() {
            return obtenerPorcentaje(this.datosFormulario.dias)
        },
        resultados() {
            return obtenerResultadosCalculos(this.datosFormulario, this.porcentaje)
        }
    },
}
</script>

<template>
    <h2>Resultados</h2>
    <ul id="resumen-datos">
        <li><span class="bold">Nombre: </span>{{datosFormulario.nombre}} {{datosFormulario.apellido}}</li>
        <li><span class="bold">Capital inicial: </span>${{datosFormulario.monto}}</li>
        <li><span class="bold">Plazo: </span>{{datosFormulario.dias}} días</li>
        <li><span class="bold">Tasa aplicada: </span>{{porcentaje}}%</li>
    </ul>
    <div id="tabla-container">
        <table id="resultados-calculos">
            <thead>
                <tr>
                    <th>Período</th>
                    <th>Monto inicial</th>
                    <th>Monto final</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="resultado in resultados">
                    <td>{{ resultado.periodo}}</td>
                    <td>{{ resultado.montoInicial.toFixed(2) }}</td>
                    <td>{{ resultado.montoFinal.toFixed(2) }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style>
#resultados-container h2 {
    text-align: center;
    font-size: 2rem;
}

#resumen-datos {
    list-style-type: none;
    margin: 10px 0;
    border: solid 2px #2C3E50;
    background-color: #58b7c5bd;
}

#resumen-datos li {
    padding: 3px;
}
#resumen-datos li:nth-child(even) {
    background-color: rgb(247, 247, 247);
}

.bold {
    font-weight: bold;
}

#tabla-container {
    height: 100%;
}

table {
    text-align: center;
    table-layout: fixed;
    width: 100%;
    border-collapse: collapse;
    background-color: #58b7c5bd;
    border: solid 2px #2C3E50;
  }

th, td {
    border-right: solid 2px #2C3E50;
    padding: 0.5%;
}

th {
    color: white;
    background-color: #222;
}

tbody tr:nth-child(odd) {
    background-color: rgb(247, 247, 247);
}
</style>