<script>
    import { slide } from "svelte/transition";

    // svelte-ignore unused-export-let
    export const key = "";
    // svelte-ignore unused-export-let
    export const options = {};

    let showInfo = false;
</script>

<button
    type="button"
    class="inline-flex txt-sm flex-gap-5 link-hint"
    on:click={() => {
        showInfo = !showInfo;
    }}
>
    <strong class="txt">String value normalizations</strong>
    {#if showInfo}
        <i class="ri-arrow-up-s-line txt-sm" />
    {:else}
        <i class="ri-arrow-down-s-line txt-sm" />
    {/if}
</button>

{#if showInfo}
    <div class="block" transition:slide|local={{ duration: 150 }}>
        <div class="alert alert-warning m-b-0 m-t-10">
            <div class="content">
                In order to support seamlessly both <code>application/json</code> and
                <code>multipart/form-data</code>
                requests, the following normalization rules are applied if the <code>json</code> field is a
                <strong>plain string</strong>:
                <ul>
                    <li>"true" is converted to the json <code>true</code></li>
                    <li>"false" is converted to the json <code>false</code></li>
                    <li>"null" is converted to the json <code>null</code></li>
                    <li>"[1,2,3]" is converted to the json <code>[1,2,3]</code></li>
                    <li>{'"{"a":1,"b":2}"'} is converted to the json <code>{'{"a":1,"b":2}'}</code></li>
                    <li>numeric strings are converted to json number</li>
                    <li>double quoted strings are left as they are (aka. without normalizations)</li>
                    <li>any other string (empty string too) is double quoted</li>
                </ul>
                Alternatively, if you want to avoid the string value normalizations, you can wrap your data inside
                an object, eg.<code>{'{"data": anything}'}</code>
            </div>
        </div>
    </div>
{/if}
