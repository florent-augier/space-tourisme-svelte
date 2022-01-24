<script context="module">
    // main navigation for the application
    import Home from "./Home.svelte";
    import Crew from "./Crew.svelte";
    import Technology from "./Technology.svelte";
    import Destination from "./Destination.svelte";
    // these are our 'pages' to navigate through (in order for this export to work the script tag MUST include context="module")
    export const navOptions = [
        { page: "HOME", component: Home, url: "#home" },
        { page: "DESTINATION", component: Destination, url: "#destination" },
        { page: "CREW", component: Crew, url: "#crew" },
        { page: "TECHNOLOGY", component: Technology, url: "#technology" },
    ];
</script>
