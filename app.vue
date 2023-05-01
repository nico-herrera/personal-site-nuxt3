<template>
	<NuxtPage />
</template>

<script setup>
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { ScrollToPlugin } from "gsap/ScrollToPlugin";
import { TextPlugin } from "gsap/TextPlugin";

import "./assets/css/main.css";

gsap.registerPlugin(ScrollTrigger, ScrollToPlugin, TextPlugin);
</script>
