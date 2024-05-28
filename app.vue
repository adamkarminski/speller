<template>
	<div
		class="flex items-center justify-center h-dvh w-dvw bg-emerald-900 text-gray-50 font-extrabold text-9xl uppercase"
	>
		{{ text }}
	</div>
</template>

<script setup lang="ts">
	const text = ref('Naciśnij jakiś klawisz');

	function speak(text: string) {
		const speech = useSpeechSynthesis(text, { lang: 'pl-PL' });
		speech.speak();
	}

	onKeyStroke(
		true,
		(e) => {
			text.value = e.key;
			speak(text.value);
		},
		{ dedupe: true }
	);

	onMounted(() => {
		speak(text.value);
	});
</script>
