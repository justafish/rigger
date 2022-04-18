<script>
	let height = 500;
	let rigger = 50;
	let legs = 100;
	let span = 157;
	let oarLength = 285;
	let inboard = 86;
	$: outboard = oarLength - inboard;
	$: width = (outboard * 2) + span + 6;
	$: offset = outboard;
	$: boatLength = 250;
	$: leftGate = (width - span) / 2;
	$: rightGate = ((width - span) / 2) + span;
	$: overlap = inboard - (span / 2);
</script>

<div class="wrapper">
	<svg width="{width}" height="{height}" version="1.1" xmlns="http://www.w3.org/2000/svg">
		<defs>
			<clipPath id="cut-off-left">
      	<rect x="0" y="0" width="{width / 2}" height="{height}" />
    	</clipPath>
    	<clipPath id="cut-off-right">
      	<rect x="{width / 2}" y="0" width="{width / 2}" height="{height}" />
    	</clipPath>
  	</defs>
		<!-- Boat -->
		<line x1="{width / 2}" x2="{width / 2}" y1="{offset}" y2="{boatLength + offset}" stroke="black" stroke-width="5"/>
		<!-- Rigger -->
		<line x1="{leftGate}" x2="{rightGate}" y1="{rigger + offset}" y2="{rigger + offset}" stroke="black" stroke-width="5"/>
		<!-- Left outboard arc -->
		<circle cx="{leftGate}" cy="{rigger + offset}" r="{outboard}" fill="none" stroke="grey" stroke-width="3" clip-path="url(#cut-off-left)" />
		<!-- Right outboard arc -->
		<circle cx="{rightGate}" cy="{rigger + offset}" r="{outboard}" fill="none" stroke="grey" stroke-width="3" clip-path="url(#cut-off-right)" />
		<!-- Left inboard arc -->
		<circle cx="{leftGate}" cy="{rigger + offset}" r="{inboard}" fill="none" stroke="grey" stroke-width="3" />
		<!-- Right inboard arc -->
		<circle cx="{rightGate}" cy="{rigger + offset}" r="{inboard}" fill="none" stroke="grey" stroke-width="3" />
		<!-- Left oar -->
		<line x1="{leftGate + inboard}" x2="{leftGate + inboard -oarLength}" y1="{rigger + offset}" y2="{rigger + offset}" stroke="green" stroke-width="3"/>
		<!-- Right oar -->
		<line x1="{rightGate - inboard}" x2="{rightGate - inboard + oarLength}" y1="{rigger + offset}" y2="{rigger + offset}" stroke="red" stroke-width="3"/>
	</svg>
</div>

<div>
  <label>
	  <div class="label">Span</div>
	  <input type=number bind:value={span} min=150 max=165>
	  <input type=range bind:value={span} min=150 max=165 step="0.5">
  </label>
	<label>
	  <div class="label">Inboard</div>
	  <input type=number bind:value={inboard} min=80 max=95>
	  <input type=range bind:value={inboard} min=80 max=95 step="0.5">
  </label>
	<label>
	  <div class="label">Oar Length</div>
	  <input type=number bind:value={oarLength} min=278 max=292>
	  <input type=range bind:value={oarLength} min=278 max=292 step="0.5">
  </label>
	<div>
		<span class="label">Handle Overlap</span>
		<span>{overlap}</span>
	</div>
	<div>
		<span>Load</span>
		<span>{outboard / inboard}</span>
	</div>
  <label>
		<div class="label">Rigger Position</div>
	  <input type=number bind:value={rigger} min=100 max=180>
	  <input type=range bind:value={rigger} min=100 max=180>
  </label>
</div>

<style>
	.wrapper {
		display: flex;
		justify-content: center;
	}
</style>

