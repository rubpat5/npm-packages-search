<template>
	<v-footer
		dark
		padless
	>
		<v-card
			flat
			tile
			class="primary white--text text-center"
			width="2000"
		>
			<v-card-text class="white--text">
				<v-row align="center" justify="center">
					<v-col class="xs-4 text-center">
						Author: Ruben Patvakanyan
					</v-col>
					<v-col class="xs-4">
						<v-avatar>
							<img
								src="https://lh3.googleusercontent.com/pw/ACtC-3cMQPisP9wiQdG0iC6_UhuV_UWB9d0bFg1gKgIwD0OhGFZo3WGRtn5FgjvOwwUsuxZvX0SS6VN3CriDwDqGJVkqREtW8S5saA3uEXy_gIEvN8ECMq4nbE1mTaf_aIQr2MVzhZ-19nJxt_bw3W5C0tEG=w1604-h1764-no?authuser=0"
								alt="Rub"
							>
						</v-avatar>
					</v-col>
					<v-col class="xs-4">
						<v-btn
							class="mx-4 white--text"
							icon
							href="https://github.com/rubpat5"
							target="_blank"
						>
							<v-icon size="24px">mdi-github</v-icon>
						</v-btn>
					</v-col>
				</v-row>
			</v-card-text>

			<v-divider></v-divider>

			<v-card-text class="white--text">
				{{ new Date().getFullYear() }} — <strong>Vuetify</strong>
			</v-card-text>
		</v-card>
    </v-footer>
</template>