---
theme: seriph
# random image from a curated Unsplash collection by Anthony (see https://unsplash.com/collections/94734566/slidev)
background: https://images.unsplash.com/photo-1619075120156-f5729c752edf?q=80&w=1742&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D
title: K8s Adversary Emulation
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# open graph
# seoMeta:
#  ogImage: https://cover.sli.dev
---

# K8s Adversary Emulation

<p class="text-xl">Adopting an Attacker's Mindset for Kubernetes Security</p>


<!-- <div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div> -->

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: intro
transition: fade-out
---

# Whoami

### Markus Gierlinger
<!-- <h3> Markus Gierlinger</h3> -->
<br/>

<div class="flex items-center gap-2">
  <img src="./assets/cast_ai_logo.jpg" class="rounded w-6 "/>
  <span> Product Manager @ Cast AI </span>
</div>

<div class="flex items-center gap-2 mt-2">
  <img src="./assets/dt.webp" class="rounded w-6 "/>
  <span> Former security researcher @ Dynatrace </span>
</div>


Enjoys exploring cybersecurity and AI 


<div>
    <a href="https://github.com/Magier" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
    <span class="ml-2">Magier</span>
  </a>
  <a href="https://www.linkedin.com/in/markus-gierlinger/" target="_blank" class="slidev-icon-btn">
    <carbon:logo-linkedin />
    <span class="ml-2">Markus</span>
  </a>
</div>

<img src="./assets/me.jpg" class="rounded-full w-64 abs-tr mt-16 mr-12"/>



---
layout: intro
---

# Whois Molly?

- New and only **SecOps Engineer** at Wish Ltd.
  - Wish Ltd. has ~300 employees
  - Heavy use of Kubernetes
- Previously ~3 years experience as SRE
- Responsible for “securing” the product


<img src="./assets/molly.jpeg" class="rounded-full w-64 abs-tr mt-16 mr-30"/>

<!-- ... instead, let met introduce you to Molly,
Molly is a newly hired SecOps Engineer at Wish Ltd.
The company has about 300 employees and is heavily using Kubernetes.
-->

---
layout: fact
---

# What does "secure" mean?



---
layout: image
image: ./assets/cncf-landscape.png
backgroundSize: contain
---

<!-- Molly is no stranger to the CNCF landscape, 
so she goes there to find tools that can help her 
... and there is certainly no shortage of tools to choose from
-->

---
transition: slide-up
---

## Defense in Depth



<img src="./assets/swiss_cheese_model.svg" class="w-full bg-white h-90 mt-10" />
<v-clicks>
<img src="./assets/trivy-black.png" class="absolute bg-white h-20 top-59 left-74" />
<img src="./assets/k8s.png" class="absolute bg-white h-20 top-59 left-102" />
<img src="./assets/falco.png" class="absolute bg-white h-20 top-59 left-130" />
</v-clicks>



---

# Endless list of findings

<v-clicks>

<img src="./assets/trivy_findings.png" class="w-150" />

<img src="./assets/falco_findings.png" class="w-150 absolute top-35 left-60" />

</v-clicks>


---
layout: image
image: ./assets/overwhelmed.jpg
title: overwhelmed
---

---
layout: fact
transition: slide-up
title: secure?
---

# Does _this_ make our environments secure?

<!-- So, she's still can't confidently answer this question, so she does some more research ... -->


---
layout: fact
transition: slide-up
title: Lambert's Quote
---

<div class="text-5xl">
"Defenders think in lists.   <br>
Attackers think in graphs.   <br>
As long as this is true, attackers win"  
</div>

<a href="https://github.com/JohnLaTwC/Shared/blob/master/Defenders%20think%20in%20lists.%20Attackers%20think%20in%20graphs.%20As%20long%20as%20this%20is%20true%2C%20attackers%20win.md" target="_blank" class="text-sm text-gray" >John Lambert, VP Security @ Microsoft, 2015</a>

<!-- ... until she finds this quote by John Lambert from 2015. -->


---
layout: image
image: ./assets/hacker-backside.jpg
title: hacker' mindest
---

<!-- This is makes Molly think ...
Security is all about preventing attacks, right?
So, by looking at the environment through the eyes of an attacker, she can actually answer the question!
-->



---
layout: two-cols-header
---

# Threat Intelligence

::left::

<!-- <img src="./assets/wiz-cloud-threat-landscape.png" class="w-99" /> -->
<img src="./assets/wiz-cloud-incidents.png" class="w-99 -mt-30" />
<a href="https://www.wiz.io/cloud-threat-landscape" target="_blank" class="text-xs">Wiz' Cloud Threat Landscape</a>


::right::
<img src="./assets/scarleteel.webp" class="w-99 -mt-20" />
<a href="https://https://sysdig.com/blog/scarleteel-2-0/" target="_blank" class="text-xs">Sysdig: Scarleteel 2.0</a>

<!---
Now, to be able to put herself into the shoes of an attacker, she needs to learn about them and their motivations.
So she does some more research and finds resources like Wiz' Cloud Threat Landscape, which is a database of notetworthy attacks. And a lot of other blog posts analyzing attacks

Does this this now mean Molly has to spend hours reading up on all types of attack reports?
-->


---

# MITRE ATT&CK


<div id="mark-tactics" v-mark="{ at: [1,2], color: 'red', type: 'box', strokeWidth: 5 }" class="w-220 -ml-1 h-12 absolute"></div>
<div id="mark-exploit-ttp" v-mark="{ at: 2, color: 'red', type: 'box', strokeWidth: 5 }" class="w-17  h-14 absolute top-38 left-14"></div>

<div id="mark-user-exec" v-mark="{ at: 3, color: 'red', type: 'box', strokeWidth: 5 }" class="w-19 h-8 absolute top-69 left-37"></div>
<arrow v-click="3" x1="125" y1="209" x2="146" y2="273" color="red" width="2" arrowSize="3" />

<div id="mark-cred-access" v-mark="{ at: 4, color: 'red', type: 'box', strokeWidth: 5 }" class="absolute top-47 left-143 w-19  h-12"></div>
<arrow v-click="4" x1="125" y1="180" x2="568" y2="200" color="red" width="2" arrowSize="3" />

<div id="mark-deploy-container" v-mark="{ at: 5, color: 'red', type: 'box', animate: false, strokeWidth: 5 }" class="absolute top-50 left-37 w-19 h-9"></div>
<arrow v-click="5" x1="568" y1="210" x2="229" y2="215" color="red" width="2" arrowSize="3" />

<div id="mark-impact" v-mark="{ at: 6, color: 'red', type: 'box', animate: false, strokeWidth: 5 }" class="absolute top-85 right-15 w-18 h-8"></div>
<arrow v-click="6" x1="229" y1="225" x2="844" y2="350" color="red" width="2" arrowSize="3" />

<img src="./assets/mitre-attack-containers.png" class="w-220"/>
<a href="https://attack.mitre.org/matrices/enterprise/containers/" target="_blank" class="text-xs">MITRE ATT&CK - Containers Matrix</a>

<!--

... Thankfully no!! Mitre, the organization behind  our beloved vulnerbailit identifiers is actually constantly analyzing and cataloging all known attacks and organizes them in the so-called ATT&CK framework.

The idea is, that any attack can be broken down into several high-level phases - so-called tactics.
And at every phase of the attack attackers have a certain set of techniques they usually use.

For example, exploit a public facing app. 
And for every technique, the actual implementation of an attack is called a "procedure".

This triple of tactics, techniques and procedures is commonly called a TTP. 
What you see here, is actually a version of the ATT&CK framework specifically for containerized environments.

What Molly can do now, is use this and try to play out scenarios. For example: once an attacker has access to a container, they can execute commands as a user ... or in K8s, read the SA token mounted inside the pod.
If the token has the permissions, the attacker can create a new pod, which may containe a cryptominer. So the final goal would be to mine crypto currency at the customers dime.

This chain of steps of TTPs is called an attack path ...
-->

---

# Attack Graph

= combination of TTPs


<div grid="~ cols-2 gap-2" m="t-2">

<div v-click class="-top-200">

#### Resource-centric

<br>

<img border="rounded" src="./assets/topology-attack-graph.png" class="h-80">

</div>

<div v-click>
  
#### Attack-centric
<br>
<img border="rounded" src="./assets/attack-flow.png" class="h-80">
</div>

</div>

<!--

... an attack graph!

For completeness: there are actually 2 flavors of graphs:
- a resource-centric one that focuses on the resources, and the attacker steps are the edges in-between
- or a attack-centric one, which focuses on the TTPs and the edges often have not much meaning

The preferred one usually depends on the use case. For example, Molly, as a defender would care more about the resource-centric graph
-->


---
layout: image-right
image: ./assets/abstract-apa.jpg
backgroundSize: contain
---

# Attack Path Analysis 

<v-clicks class="text-2xl mt-20 space-y-4">

- _Models_ all possible attack paths
- Full visiblity of environment
- Contextualizes findings
- Enables advanced analysis

</v-clicks>


---
layout: two-cols
---
# Attack Path Analysis Tools


<div class="flex items-center justify-between -mb-5">
  <a href="https://github.com/ReversecLabs/IceKube" class="text-m">IceKube</a>
  <img src="./assets/icekube.png" class="w-32 mr-30" />
</div>

<v-clicks >

- 25 TTPs 
- uses Neo4J 
- Query using Cypher

<img src="./assets/icekube_example.webp" class="w-70 bg-blend-lighten icekube-example mt-2" />

</v-clicks>

::right::


<v-clicks class="">

<div class="flex items-center justify-between mt-15">
  <a href="https://kubehound.io/">KubeHound</a>
  <img src="./assets/kubehound.png" class="w-30 mr-30" />
</div>

  - 25 TTPs 
  - uses JanusGraph 
  - Jupyter Notebook for analysis
  - experimental automation features 

</v-clicks>

<style>
.icekube-example {
  background-color:rgba(240, 240, 240, 0.2);
  border-radius: 8px;
  padding: 10px;
}
</style>


--- 
class: px-10
layout: two-cols-header
---

# Getting real

<!-- <div grid="~ cols-2 gap-2" m="t-2"> -->
::left::

<div v-click.hide="1" class="dimmed">
  <!-- <span class="dimmed">Attack Path Analysis</span> -->

# Attack Path Analysis 
<!-- - Models attack -->
<!-- - Full visiblity -->

<img src="./assets/abstract-apa.jpg" class="w-99 " />

</div>

::right::

<v-click>

# Adversary Emulation

<!-- - Performs attack
- limited visibility -->

<img src="./assets/emulation-abstract.jpg" class="w-99 " />

</v-click>


::bottom::

<br>
<br>
<br>

<style>
/* .dimmed {
  opacity: 0.3;
} */

.slidev-vclick-hidden.dimmed {
  opacity: 0.3 !important;
  /* transform: scale(0); */
}
</style>

---
transition: slide-up
---

# Adversary Emulation

- Perform attack on real environments

- Evalates the effectiveness of security controls

- Varying degree of realism:

<img src="./assets/emulation-spectrum.png" class="w-full mt-20" />

---
level: 2
---

# Atomic Emulation

<div class="pr-10">

- detonate single TTPs
- primarily use-case:
  - test processing pipeline
  - manage detections  
</div>



<div v-click class="mt-5">

#### Tools

<div class="flex gap-10">
  <div v-click=1>
  <div class="flex items-center justify-between gap-20">
    <a href="https://github.com/redcanaryco/atomic-red-team">Atomic Red Team</a>
    <img src="./assets/atomic-red-team.png" class="w-24 mr-30" />
  </div>

  - [1700+ TTPs](https://www.atomicredteam.io/atomic-red-team)
  - focus on OS-based TTPs
  - ~10 TTPs for Docker + K8s 

  </div>


  <div v-click=2 >
  <div class="flex items-center justify-between gap-20">
    <a href="https://github.com/DataDog/stratus-red-team">Stratus Red Team</a>
    <img src="./assets/stratus-red-team.png" class="w-25" />
  </div>

  - [50+](https://www.atomicredteam.io/atomic-red-team) 
  - focuses on AWS, Azure, GCP
  - ~8 TTPs for K8s 
  </div>
</div>
</div>

<!-- e.g. is everything working properly, after installing a detection tool? -->


---
layout: image
---

<img src="./assets/stratus-red-team-demo.gif" class="w-full" />

---

# Planned Emulation

<div class="flex gap-10">
<!-- <div class="grid grid-cols-2 gap-10"> -->
<div >

- aka "[Micro emulations](https://ctid.mitre.org/projects/micro-emulation-plans/)"

<v-clicks >

- easy to automate
- Validate atomic + chain analytics
- good for reproducing scenarios

</v-clicks>

</div>
<img src="./assets/attack-flow.png" class="w-130 -mt-10" />

</div>

---

# Planned Emulation: Tools

<div class="grid grid-cols-2 gap-10">

<div class="mt-10">
<div class="flex items-center justify-between ">
<h3> <a href="https://github.com/mitre/caldera">Mitre Caldera</a> </h3>
  <img src="./assets/caldera-logo.png" class="w-32 mr-10" />
</div>

<v-clicks class="mt-2">

- oldest and most mature emulation tool (2015)
- primary for enterprise environments
- no special K8s support
- big plugin ecosystem
- supports automated planning

</v-clicks>
</div >

<div class="mt-17">


<h3 v-click>
<a href="https://github.com/ReversecLabs/leonidas">Leonidas</a>
</h3>


<v-clicks class="mt-10">

- similar to Stratus Red Team
- allows chaining of TTPs
- runs as workload inside K8s cluster
- supports only `kubectl`-based TTPs for K8s

</v-clicks>

</div>

</div>

---

# Realistic Emulation

<div class="grid grid-cols-3 gap-10">

<div class="col-span-2 mt-10">

<v-clicks>

- "Fog of War"

<img src="./assets/ooda-loop.png" class="absolute w-40 top-25 left-80" />

- a red team engagement

</v-clicks>




<v-clicks class="mt-20">

<h4 class="mt-15 mb-2">Use Cases</h4>

- Evaluate incident response plans
- testing more sophisticated defenses
    - Moving Target Defense
    - Deception
</v-clicks>

<div v-click class="i-game-icons:drama-masks text-30 text-blue-200 w-full -mt-3">
</div>

</div>

<div v-click=7 class="flex flex-col text-center items-center justify-center gap-5">

## Tools

<img src="./assets/caldera-logo.png" class="w-32" />

<br>
<br>

<v-click at="8">
<img src="./assets/ran.svg" class="w-32" />
<a  href="https://github.com/magier/ran">Ran</a>
</v-click>

</div>

</div>




---
layout: fact
---

# Demo



--- 

# Take-aways



<div class="rounded-lg bg-sky-600 border-l-4 border-sky-900 p-4 my-6 text-blue-200 shadow-md">
   Adopt an attacker's mindset to assess your effective security.
</div>


<div class="grid grid-cols-2 gap-10">
<div class="rounded-lg bg-sky-700 border-l-4 border-sky-900 p-4 my-6 text-blue-200 shadow-md">
  <h3 class="mb-2">Attack Path Analysis</h3>

  - Contextualize security findings
  - Uncover dangerous combinations
  - Plan for improvements

  <div class="i-game-icons:path-distance text-30 text-blue-200 w-full mt-3"></div>
</div>


  <div class="rounded-lg bg-sky-700 border-l-4 border-sky-900 p-4 my-6 text-blue-200 shadow-md">
    <h3 class="mb-2">Adversary Emulation</h3>

  - Validate security controls
  - Improve detection & response
  - Show value of more advanced defenses

  <div class="i-game-icons:gamepad text-30 text-blue-200 w-full mt-3"></div>
  </div>
</div>