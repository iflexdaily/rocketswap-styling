<script lang="ts">
    import { createEventDispatcher } from 'svelte'

	//Services
	import { ApiService } from '../../services/api.service'
	const apiService = ApiService.getInstance();

    const dispatch = createEventDispatcher();

    let inputValue;
    let timer;

    const handleInput = (e) => {
        clearTimeout(timer)
        timer = setTimeout(getToken, 500);
    }

    const getToken = async () => {
        let tokenRes = await apiService.getToken(inputValue)
        dispatchEvent(tokenRes)
    }

    const dispatchEvent = (searchResult) => {
        dispatch('search', {inputValue, searchResult})
    }
</script>

<style>
    input{
        background-color: transparent;
        border: none;
        color: var(--text-primary);
        padding: 0;
    }
    ::placeholder { 
        color: rgb(168, 178, 199);
        opacity: 1; 
    }
    :-ms-input-placeholder { 
        color: rgb(168, 178, 199);
    }
    ::-ms-input-placeholder { 
        color: rgb(168, 178, 199);
    }
</style>

<input 
    placeholder="Token Name or Contract"
    bind:value={inputValue}
    on:input={handleInput}
/>
