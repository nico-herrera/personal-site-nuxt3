<script setup>
import { onMounted, onUnmounted, ref } from "vue";
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

const main = ref();
let ctx;

const year = new Date().getFullYear();

onMounted(() => {
	const tl = gsap.timeline({ repeat: -1, repeatDelay: 1, yoyo: true });
	const tween = gsap.to("#name", {
		duration: 2,
		ease: "none",
		text: { value: "Full-Stack Web Developer" },
	});

	tl.add(tween);

	gsap.set(".single-step", { autoAlpha: 0 });

	const pinDistance = 2000;

	/* section */
	ScrollTrigger.create({
		trigger: ".two",
		start: "top top",
		end: "+=" + pinDistance,
		pin: ".wrapper",
		id: "two",
	});

	/* texts inside section */
	const stepsTimeline = gsap.timeline({
		scrollTrigger: {
			trigger: ".two .stepped-animation",
			start: "top top",
			end: "+=" + pinDistance,
			scrub: true,
		},
	});

	const steps = gsap.utils.toArray(".two .single-step");

	// loop through each step and add a callback into the timeline, spaced equally (1 second apart just to make things simple)
	steps.forEach((step, i) => {
		stepsTimeline.add(() => {
			// if scrolling backward, we need to invert which element fades in or out
			const forward = stepsTimeline.scrollTrigger.direction > 0,
				inEl = forward ? step : steps[i - 1],
				outEl = forward ? steps[i - 1] : step;
			outEl && gsap.to(outEl, { autoAlpha: 0, duration: 0.3, overwrite: true });
			inEl &&
				gsap.to(inEl, {
					autoAlpha: 1,
					duration: 0.3,
					delay: 0.3,
					overwrite: true,
				});
		}, i || 0.001);
	});
	// add blank space to the end of the timeline so that the last element stays for a bit before unpinning.
	stepsTimeline.to({}, { duration: 1 });
});

onUnmounted(() => {
	ctx.revert(); // <- Easy Cleanup!
});
</script>

<template>
	<main class="bg-slate-900 relative tracking-wider">
		<header class="sticky top-0 shadow-md backdrop-blur-md z-10">
			<nav
				class="hidden md:flex text-lg text-gray-100 justify-between items-center h-[6vh] px-8 w-full"
			>
				<h1 class="w-1/2 text-2xl">
					<a href="#home">Nico Herrera</a>
				</h1>
				<ul class="flex justify-between items-center w-1/4">
					<li>
						<a href="#home">Home</a>
					</li>
					<li>
						<a href="#about">About</a>
					</li>
					<li>
						<a href="#passions">Passions</a>
					</li>
					<li>
						<a href="#contact">Contact</a>
					</li>
				</ul>
			</nav>
		</header>
		<section
			id="home"
			class="h-screen md:h-[94vh] flex items-center justify-center"
		>
			<div class="px-8 py-32">
				<div class="grid gap-8 items-start justify-center">
					<div class="relative group">
						<div
							class="absolute -inset-0.5 bg-gradient-to-r from-green-600 to-indigo-600 rounded-lg blur opacity-75 group-hover:opacity-100 transition duration-1000 group-hover:duration-200 animate-tilt"
						></div>
						<button
							class="relative px-7 py-4 bg-slate-900 rounded-lg leading-none flex items-center divide-x divide-gray-600"
						>
							<h1 id="name" class="text-4xl md:text-6xl text-gray-100 font-bold"
								>Nico Herrera</h1
							>
						</button>
					</div>
				</div>
			</div>
		</section>

		<div class="wrapper relative px-4 md:px-0">
			<span id="about" class="absolute -top-20"></span>

			<section class="two h-screen w-full">
				<div id="scroll-container" class="h-full">
					<div
						class="stepped-animation h-full overflow-y-auto relative text-2xl text-gray-100 flex items-start md:justify-center md:items-center flex-col"
					>
						<div
							class="flex items-center justify-center flex-col mt-4 md:mt-0 md:mb-72"
						>
							<h2
								class="text-3xl md:text-5xl font-bold mb-2 md:mb-6 text-center"
								>Who is Nico?</h2
							>
							<p class="text-center mb-3 text-xl md:text-2xl"
								>Hello, thanks for visiting my website! Scroll to learn about
								me.
							</p>
						</div>
						<div
							class="single-step flex justify-center items-center absolute top-0 left-0 w-full h-full opacity-0"
						>
							<div class="single-step__inner w-full md:w-1/2 p-4 indent-6">
								I'm a
								<span class="text-green-500">full stack web developer</span>
								with a passion for creating awesome digital experiences. I've
								been in the game for several years now and I absolutely love
								what I do.
							</div>
						</div>
						<div
							class="single-step flex justify-center items-center absolute top-0 left-0 w-full h-full opacity-0"
						>
							<div class="single-step__inner w-full md:w-1/2 p-4 indent-6">
								I'm fluent in a variety of programming languages and frameworks,
								including <span class="text-green-500">JavaScript</span>,
								<span class="text-green-500">React</span>,
								<span class="text-green-500">SvelteKit</span>,
								<span class="text-green-500">Node.js</span>,
								<span class="text-green-500">MongoDB</span> and
								<span class="text-green-500">SQL</span>. This site in
								particuluar was built using
								<span class="text-green-500">NuxtJS</span>. I've built
								everything from e-commerce sites to complex web applications,
								and I'm always eager to take on new challenges.
							</div>
						</div>

						<div
							class="single-step flex justify-center items-center absolute top-0 left-0 w-full h-full opacity-0"
						>
							<div class="single-step__inner w-full md:w-1/2 p-4 indent-6">
								What I love most about web development is the
								<span class="text-green-500"
									>opportunity to bring people's ideas to life</span
								>. Whether it's a simple landing page or a complex web app,
								there's something
								<span class="text-indigo-500">incredibly satisfying</span> about
								taking a concept from the drawing board to the screen.
							</div>
						</div>

						<div
							class="single-step flex justify-center items-center absolute top-0 left-0 w-full h-full opacity-0"
						>
							<div class="single-step__inner w-full md:w-1/2 p-4 indent-6">
								Outside of work, you can usually find me
								<span class="text-green-500"
									>tinkering with new technologies</span
								>,
								<span class="text-green-500">helping new developers </span>with
								their journey, or something sports related. I'm a firm believer
								that the best developers are always learning, and I'm
								<span class="text-indigo-500">constantly pushing myself</span>
								to stay up-to-date with the latest trends and best practices.
							</div>
						</div>

						<div
							class="single-step flex justify-center items-center absolute top-0 left-0 w-full h-full opacity-0"
						>
							<div class="single-step__inner w-full md:w-1/2 p-4 indent-6">
								If you're looking for a
								<span class="text-green-500">passionate</span>,
								<span class="text-green-500">experienced</span>, and
								<span class="text-green-500">all-around awesome</span> full
								stack web developer , look no further! Let's chat and see what
								we can create together.
							</div>
						</div>
					</div>
				</div>
			</section>
		</div>

		<section class="p-8 relative mb-40 md:mb-64">
			<span id="passions" class="absolute -top-20"></span>

			<div
				class="flex items-start justify-start flex-col text-gray-100 h-full w-full md:w-1/2 mx-auto"
			>
				<h2 class="text-4xl md:text-5xl font-bold mb-6">Current Passions!</h2>
				<p class="text-xl md:text-center mb-3"
					>Here's a few things I'm learning right now.
				</p>
				<div class="flex flex-col gap-6 mt-6">
					<div class="flex flex-col gap-1">
						<h4 class="text-indigo-500 text-3xl">Machine Learning</h4>
						<p
							>Currently, I'm learning about Neural Networks and several other
							methods of machine learning. One of my goals is to make my own
							image classification model that can give niche labels to different
							pieces of art.</p
						>
					</div>
					<div class="flex flex-col gap-1">
						<h4 class="text-indigo-500 text-3xl">Web3 Smart Contracts</h4>
						<p
							>As a web3 developer, I interact with data from the blockchain
							every day. One of the things I'm working towards is being able to
							write very secure Smart Contracts, and maybe even help companies
							expose weaknesses in their own.</p
						>
					</div>

					<div class="flex flex-col gap-1">
						<h4 class="text-indigo-500 text-3xl">Green Sock Animations</h4>
						<p
							>Not sure if you couldn't tell already, but some of my site uses
							GSAP, and I'm striving towards being able to build a smooth and
							seamless site with plenty of animations and only requires the user
							to scroll, read, and be amazed.</p
						>
					</div>

					<div class="flex flex-col gap-1">
						<h4 class="text-indigo-500 text-3xl">Blogging</h4>
						<p
							>We were onced assigned to write a blog post about our journey as
							a developer in school, and from there I discovered that I actually
							enjoyed writing. I think it could be beneficial to other
							developers if they could read about another developers
							experiences. So, I've made it a goal of mine to try and write one
							blog per month.</p
						>
					</div>
				</div>
			</div>
		</section>
		<section id="contact" class="mb-20">
			<div class="flex items-center justify-center flex-col text-gray-100">
				<h2 class="text-5xl font-bold mb-6">Let's Connect!</h2>
				<p class="text-xl text-center mb-10"
					>Have a question or want to work together? Feel free to reach out!
				</p>
				<div class="flex flex-col md:flex-row gap-8 text-indigo-500 text-2xl">
					<a
						class="bg-slate-800 rounded-md px-8 py-2 hover:text-green-500 transition ease-in-out"
						target="_blank"
						href="mailto:nicoherrera0831@gmail.com?subject=I%20like%20your%20style!"
						>Email</a
					>
					<a
						class="bg-slate-800 rounded-md px-8 py-2 hover:text-green-500 transition ease-in-out"
						target="_blank"
						href="https://www.linkedin.com/in/nicoherreradev/"
						>LinkedIn</a
					>
					<a
						class="bg-slate-800 rounded-md px-8 py-2 hover:text-green-500 transition ease-in-out"
						target="_blank"
						href="/resume.pdf"
						>Resume</a
					>
				</div>
			</div>
		</section>
		<footer class="h-20 bg-slate-800 flex items-center pl-6">
			<div class="text-base text-gray-100"> © Nico Herrera {{ year }} </div>
		</footer>
	</main>
</template>
<style>
.container {
	width: 100%;
	overflow-x: auto;
	white-space: nowrap;
	background-color: #eee;
}

.content {
	display: inline-block;
}

.item {
	display: inline-block;
	width: 100vw;
	height: 200px;
	margin-right: 10px;
	background-color: #ccc;
}
</style>
