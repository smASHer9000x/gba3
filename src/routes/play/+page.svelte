<script lang="ts">
    import { Button } from "$lib/components/ui/button";
    import { browser } from "$app/environment";
    import { base } from "$app/paths";
    import * as DropdownMenu from "$lib/components/ui/dropdown-menu";


    let game = "";
    let core = "";
    let url = "";
    let title = "";

    if (browser) {
        const urlParams = new URLSearchParams(window.location.search);
        game = decodeURIComponent(urlParams.get("game"));
        core = urlParams.get("core");
        title = decodeURIComponent(urlParams.get("title"));
        let endURL = encodeURIComponent(game)
        url = base + "/launch.html?core=" + core + "&game=" + endURL;
        console.log(url);
    }

    function toggleFullScreen() {
            if (!document.fullscreenElement) {
                document.getElementById("game").requestFullscreen();
            } else if (document.exitFullscreen) {
                document.exitFullscreen();
            }
    }

    function copyLink() {
        let newURL = window.location.origin + url;
        navigator.clipboard.writeText(newURL);
    }

    function copyEmbed() {
        let newURL = window.location.origin + url;
        navigator.clipboard.writeText("<iframe id=\"game\" class=\"overflow-hidden h-full\" title=\"Site by MSG! GBA \" src=\"" + newURL + "\" width=\"100%\" height=\"100%\" frameborder=\"0\"></iframe>");
    }
    
</script>
<svelte:head>
    <title>Playing: </title> 
</svelte:head>
    <div class="flex h-[90vh] flex-col rounded-md lg:p-12 lg:px-20 sm:p-0 sm:px-0">
    <iframe id="game" class="overflow-hidden h-full" title="Emulator" src="{url}" width="100%" height="100%" frameborder="0"></iframe>
    <div class="flex justify-between rounded-b-md bg-secondary p-4">
        <div>
            <h1 class="text-2xl font-bold mt-2">Now Playing: <Button class="p-0 text-xl font-bold" href="{game}" variant="link">{title}</Button></h1>
            <p>Core: {core}</p>
        </div>
        <div class="mt-4">
            <DropdownMenu.Root>
                <DropdownMenu.Trigger><svg class="h-6 w-6" viewBox="0 0 15 15" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M4.62471 4.00001L4.56402 4.00001C4.04134 3.99993 3.70687 3.99988 3.4182 4.055C2.2379 4.28039 1.29846 5.17053 1.05815 6.33035C0.999538 6.61321 0.999604 6.93998 0.999703 7.43689L0.999711 7.50001L0.999703 7.56313C0.999604 8.06004 0.999538 8.38681 1.05815 8.66967C1.29846 9.8295 2.2379 10.7196 3.4182 10.945C3.70688 11.0001 4.04135 11.0001 4.56403 11L4.62471 11H5.49971C5.77585 11 5.99971 10.7762 5.99971 10.5C5.99971 10.2239 5.77585 10 5.49971 10H4.62471C4.02084 10 3.78907 9.99777 3.60577 9.96277C2.80262 9.8094 2.19157 9.21108 2.03735 8.46678C2.00233 8.29778 1.99971 8.08251 1.99971 7.50001C1.99971 6.91752 2.00233 6.70225 2.03735 6.53324C2.19157 5.78895 2.80262 5.19062 3.60577 5.03725C3.78907 5.00225 4.02084 5.00001 4.62471 5.00001H5.49971C5.77585 5.00001 5.99971 4.77615 5.99971 4.50001C5.99971 4.22387 5.77585 4.00001 5.49971 4.00001H4.62471ZM10.3747 5.00001C10.9786 5.00001 11.2104 5.00225 11.3937 5.03725C12.1968 5.19062 12.8079 5.78895 12.9621 6.53324C12.9971 6.70225 12.9997 6.91752 12.9997 7.50001C12.9997 8.08251 12.9971 8.29778 12.9621 8.46678C12.8079 9.21108 12.1968 9.8094 11.3937 9.96277C11.2104 9.99777 10.9786 10 10.3747 10H9.49971C9.22357 10 8.99971 10.2239 8.99971 10.5C8.99971 10.7762 9.22357 11 9.49971 11H10.3747L10.4354 11C10.9581 11.0001 11.2925 11.0001 11.5812 10.945C12.7615 10.7196 13.701 9.8295 13.9413 8.66967C13.9999 8.38681 13.9998 8.06005 13.9997 7.56314L13.9997 7.50001L13.9997 7.43688C13.9998 6.93998 13.9999 6.61321 13.9413 6.33035C13.701 5.17053 12.7615 4.28039 11.5812 4.055C11.2925 3.99988 10.9581 3.99993 10.4354 4.00001L10.3747 4.00001H9.49971C9.22357 4.00001 8.99971 4.22387 8.99971 4.50001C8.99971 4.77615 9.22357 5.00001 9.49971 5.00001H10.3747ZM5.00038 7C4.72424 7 4.50038 7.22386 4.50038 7.5C4.50038 7.77614 4.72424 8 5.00038 8H10.0004C10.2765 8 10.5004 7.77614 10.5004 7.5C10.5004 7.22386 10.2765 7 10.0004 7H5.00038Z" fill="currentColor" fill-rule="evenodd" clip-rule="evenodd"></path></svg></DropdownMenu.Trigger>
                <DropdownMenu.Content>
                  <DropdownMenu.Group>
                    <DropdownMenu.Item on:click={copyLink}>Copy Link</DropdownMenu.Item>
                    <DropdownMenu.Item on:click={copyEmbed}>Copy Embed Code</DropdownMenu.Item>
                  </DropdownMenu.Group>
                </DropdownMenu.Content>
              </DropdownMenu.Root>
              <Button variant="ghost" on:click={toggleFullScreen}>
                <svg class="h-6 w-6" viewBox="0 0 15 15" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M2 2.5C2 2.22386 2.22386 2 2.5 2H5.5C5.77614 2 6 2.22386 6 2.5C6 2.77614 5.77614 3 5.5 3H3V5.5C3 5.77614 2.77614 6 2.5 6C2.22386 6 2 5.77614 2 5.5V2.5ZM9 2.5C9 2.22386 9.22386 2 9.5 2H12.5C12.7761 2 13 2.22386 13 2.5V5.5C13 5.77614 12.7761 6 12.5 6C12.2239 6 12 5.77614 12 5.5V3H9.5C9.22386 3 9 2.77614 9 2.5ZM2.5 9C2.77614 9 3 9.22386 3 9.5V12H5.5C5.77614 12 6 12.2239 6 12.5C6 12.7761 5.77614 13 5.5 13H2.5C2.22386 13 2 12.7761 2 12.5V9.5C2 9.22386 2.22386 9 2.5 9ZM12.5 9C12.7761 9 13 9.22386 13 9.5V12.5C13 12.7761 12.7761 13 12.5 13H9.5C9.22386 13 9 12.7761 9 12.5C9 12.2239 9.22386 12 9.5 12H12V9.5C12 9.22386 12.2239 9 12.5 9Z" fill="currentColor" fill-rule="evenodd" clip-rule="evenodd"></path></svg>
              </Button>
        </div>
    </div>
    </div>