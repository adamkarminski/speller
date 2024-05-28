<template>
	<div
		class="flex items-center justify-center h-dvh w-dvw bg-emerald-900 text-gray-50 font-extrabold uppercase"
		:class="[text === defaultText ? 'text-4xl' : 'text-9xl']"
	>
		{{ text }}
	</div>
</template>

<script setup lang="ts">
	const defaultText = 'Naciśnij jakiś klawisz';
	const text = ref(defaultText);

	function speak(text: string) {
		const speech = useSpeechSynthesis(text.toLowerCase(), {
			lang: 'pl-PL',
			rate: 0.4,
			pitch: 0.8,
		});
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
		setTimeout(() => {
			speak(text.value);
		}, 10);
	});
</script>
f
