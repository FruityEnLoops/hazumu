<script>
    import { DataTable, Image } from "smelte";
    export let data;
</script>

<main>
    <DataTable 
        {data}
        columns={[
            {label: "Message", field: "content"},
            {
                label: "Cover",
                component: Image,
                componentProps: (item) => item.attachments && item.attachments[0]
                    ? ({src: item.attachments[0].url, alt: "Cover art", class: 'h-full', height: 100})
                    : {}
            },
            {label: "Author", value: (item) => item.author.name },
        ]}
    />   
</main>

<style>
</style>