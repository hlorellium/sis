<script lang="ts">
    export let x:number;
    export let y:number;

    export let namePosition: 'top' | 'bottom' = 'top';

    export let name = '';
</script>


{#if namePosition === 'top'}
    <svg width="78" height="70" viewBox="0 0 78 70" fill="none"   {x} y={y - 18} xmlns="http://www.w3.org/2000/svg">
        <g id="tank">
            <rect id="Rectangle 1" x="0.5" y="18.5" width="77" height="51" stroke="red"/>
            <text  fill="black" xml:space="preserve" style="white-space: pre" font-family="Inter" font-size="12" letter-spacing="0em">
                <tspan x="1.55469" y="8.86364">{name}</tspan>
            </text>
            <path id="Vector 1" d="M0.325012 18.5235L77.5125 69.4765M0.325012 69.4765L77.5125 18.5235" stroke="black"/>
        </g>
    </svg>

{:else}
    <svg width="78" height="67" viewBox="0 0 78 67" fill="none"  {x} {y} xmlns="http://www.w3.org/2000/svg">
        <g id="tank">
            <rect id="Rectangle 1" x="0.5" y="0.5" width="77" height="51" stroke="red"/>
            <text  fill="black" xml:space="preserve" style="white-space: pre" font-family="Inter" font-size="12" letter-spacing="0em"><tspan x="3" y="66.8636">{name}</tspan></text>
            <path id="Vector 1" d="M0.325012 0.523499L77.5125 51.4765M0.325012 51.4765L77.5125 0.523499" stroke="black"/>
        </g>
    </svg>
{/if}
