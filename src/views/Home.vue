<style>
</style>

<template>
	<v-container class="grey lighten-5">
		<!-- Layout es como el ROW de bootstrap -->
		<v-layout :wrap="true">	
			<!-- Flex es como el COL de bootstrap -->
			<v-flex x12>
				<v-date-picker
			      v-model="fechaSeleccionada" color="green lighten-1" :full-width="true" :show-current="true" :min="diaMinimo" :max="diaMaximo" @change='getDolar(fechaSeleccionada)' ></v-date-picker>
			</v-flex xs12>	
			<v-flex xs12>	
				<v-card color="green lighten-1" dark>
					<v-card-text class="display-1 text-center">
						{{valor}}
					</v-card-text>
				</v-card>
			</v-flex>	
		</v-layout>	
	</v-container>
</template>

<script>
import { axios } from "axios";
import { mapMutations } from "vuex";

export default {
	name: 'Home',
	data () {
		return {
			fechaSeleccionada:new Date().toISOString().substr(0, 10),
			diaMinimo:'1984',
			diaMaximo:new Date().toISOString().substr(0, 10),
			valor: 0,
		}
	},
	methods: {
		...mapMutations(['mostrarLoading', 'ocultarLoading']),
		async getDolar(dia) {
			let ddmmyy = dia.split(['-']).reverse().join('-')
			try {
				this.mostrarLoading({titulo:''})
				let datos = await this.axios.get(`https://mindicador.cl/api/dolar/${ddmmyy}`)
				this.valor = await datos.data.serie[0].valor
			} catch(error) {
				this.valor = 'Fin de semana'
			} finally {
				this.ocultarLoading()
			}
		}
	},
	created() {
		this.getDolar(this.fechaSeleccionada)
	}
}
</script>
