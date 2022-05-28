<!-- https://mzaini30.js.org/nikah/#/?

	i=Fulanah&
	ki=Pak+Fulanah&
	hi=Bertanggung+jawab&

	s=Ustadz+Latif&
	ks=Pak+Fulan&
	hs=Tercantik+selalu&

	ta=Minggu,+1+Januari+2021&
	ja=08.00&
	la=rumah+wanita&

	tr=Senin,+2+Januari+2021&
	jr=09.00&
	lr=masjid 

-->

<script setup="">
	import {ref} from 'vue'
	import localforage from 'localforage'

	const i = ref('')
	const ki = ref('')
	const hi = ref('')

	const s = ref('')
	const ks = ref('')
	const hs = ref('')
	
	const ta = ref('')
	const ja = ref('')
	const la = ref('')
	
	const tr = ref('')
	const jr = ref('')
	const lr = ref('')

	async function cek(){
		let data = await localforage.getItem('dataUndanganOnline')
		if (data){
			i.value = data.i
			ki.value = data.ki
			hi.value = data.hi

			s.value = data.s
			ks.value = data.ks
			hs.value = data.hs

			ta.value = data.ta
			ja.value = data.ja
			la.value = data.la

			tr.value = data.tr
			jr.value = data.jr
			lr.value = data.lr
		}
	}
	cek()

	async function olah(){
		let link = 'https://mzaini30.js.org/nikah/'
		link = new URL(link)

		link.searchParams.set('i', i.value)
		link.searchParams.set('ki', ki.value)
		link.searchParams.set('hi', hi.value)

		link.searchParams.set('s', s.value)
		link.searchParams.set('ks', ks.value)
		link.searchParams.set('hs', hs.value)

		link.searchParams.set('ta', ta.value)
		link.searchParams.set('ja', ja.value)
		link.searchParams.set('la', la.value)

		link.searchParams.set('tr', tr.value)
		link.searchParams.set('jr', jr.value)
		link.searchParams.set('lr', lr.value)

		let simpan = await localforage.setItem('dataUndanganOnline', {
			i: i.value,
			ki: ki.value,
			hi: hi.value,

			s: s.value,
			ks: ks.value,
			hs: hs.value,

			ta: ta.value,
			ja: ja.value,
			la: la.value,

			tr: tr.value,
			jr: jr.value,
			lr: lr.value,
		})

		if (simpan){
			location.href = link.toString().replace('nikah/', 'nikah/#/')
		}
	}
</script>

<template>
	<div class="p-4">
		<form @submit.prevent='olah' action="">
			<label for="">Nama Suami</label>
			<input v-model='s' type="text" required placeholder="Fulan" />
			<label for="">Keluarga Suami</label>
			<input v-model='ks' type="text" required placeholder="Pak Fulan" />
			<label for="">Harapan Suami</label>
			<input v-model='hs' type="text" required placeholder="Istri baik hati" />

			<img src="/garis.webp" class="garis" alt="" />

			<label for="">Nama Istri</label>
			<input v-model='i' type="text" required placeholder="Fulanah" />
			<label for="">Keluarga Istri</label>
			<input v-model='ki' type="text" required placeholder="Pak Fulan" />
			<label for="">Harapan Istri</label>
			<input v-model='hi' type="text" required placeholder="Suami setia" />

			<img src="/garis.webp" class="garis" alt="" />

			<label for="">Tanggal Akad</label>
			<input v-model='ta' type="text" required placeholder="Minggu, 1 Januari 2020" />
			<label for="">Jam Akad</label>
			<input v-model='ja' type="text" required placeholder="08.00" />
			<label for="">Lokasi Akad</label>
			<input v-model='la' type="text" required placeholder="Rumah pribadi" />

			<img src="/garis.webp" class="garis" alt="" />

			<label for="">Tanggal Resepsi</label>
			<input v-model='tr' type="text" required placeholder="Minggu, 1 Januari 2020" />
			<label for="">Jam Resepsi</label>
			<input v-model='jr' type="text" required placeholder="08.00" />
			<label for="">Lokasi Resepsi</label>
			<input v-model='lr' type="text" required placeholder="Rumah pribadi" />

			<input type="submit" class="bg-pink-300 !my-8 border border-pink-700 text-pink-900 cursor-pointer block mx-auto px-5 py-1 rounded" value="Buat" />

			<a class="text-sm text-center block underline decoration-wavy text-[.7rem] mb-3 text-slate-700 font-bold uppercase" href="https://play.google.com/store/apps/details?id=com.mzaini30.undanganonline">Review aplikasi ini</a>
		</form>
	</div>
</template>

<style scoped>
	label, input {
		@apply block mb-3
	}
	input {
		@apply focus:outline-none;
	}
	[type=text]{
		@apply border border-pink-500 focus:outline-pink-500 py-1 px-2 w-full rounded
	}
	.garis {
		@apply my-6 block mx-auto w-[10rem] h-auto
	}
</style>