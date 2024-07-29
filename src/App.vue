<template>
  <div class="justify-center w-screen h-screen p-10 overflow-auto">
    <div class=" text-center ">
      <h1 class="text-5xl font-bold mb-4">Arc de Triomphe</h1>
    </div>

    <div class=" justify-center p-10  items-center w-full">
      <ThreeSixtyViewer imageUrl="/360.jpg" width="1000px" height="800px" />
    </div>

    <div class=" justify-center p-10">
      <p class="text-base  text-center">
        The Arc de Triomphe is one of the most iconic monuments in Paris,
        France. It stands majestically at the western end of the Champs-Élysées,
        at the center of the Place Charles de Gaulle, formerly known as Place de
        l'Étoile. This monumental arch, commissioned by Emperor Napoleon I in
        1806 after his victory at Austerlitz, was designed to honor those who
        fought and died for France during the French Revolutionary and
        Napoleonic Wars. The design of the Arc de Triomphe, created by architect
        Jean Chalgrin, is inspired by the grandeur of Roman architecture. The
        structure stands 50 meters (164 feet) tall, 45 meters (148 feet) wide,
        and 22 meters (72 feet) deep. It features a large central arch flanked
        by two smaller arches, with elaborate sculptures and reliefs adorning
        its facades. These include the famous "Departure of the Volunteers of
        1792," also known as "La Marseillaise," sculpted by François Rude, and
        other works depicting significant battles and events. Beneath the Arc
        lies the Tomb of the Unknown Soldier, added after World War I, which
        contains an eternal flame honoring unidentified soldiers who died in the
        war. The monument also has an observatory at the top, offering panoramic
        views of Paris. The Arc de Triomphe serves not only as a memorial to
        military triumph but also as a symbol of French national pride and a
        site for major national celebrations and events, including military
        parades and commemorations. It remains one of the most visited and
        recognized landmarks in the world.
      </p>
    </div>
  </div>
</template>

<script setup>
import ThreeSixtyViewer from "./components/ThreeSixtyViewer.vue";
</script>
