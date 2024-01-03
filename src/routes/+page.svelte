<script>
    import "../app.css";
    import Clock from "./clock.svelte";

    let image = "./background.jpg";
</script>

<div class="h-screen w-screen">
    <img src={image} alt="background" class="object-none h-screen w-screen">
</div>
<div class="fixed top-0 left-0 right-0 flex items-center h-screen">
    <Clock />
</div>
