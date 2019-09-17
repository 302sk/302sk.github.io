<div id="gitmentContainer"></div>
<link rel="stylesheet" href="https://imsun.github.io/gitment/style/default.css">
<script src="https://imsun.github.io/gitment/dist/gitment.browser.js"></script>
<script>
var gitment = new Gitment({
    owner: '302sk',
    repo: '302sk.github.io',
    oauth: {
        client_id: '182fa66dc5abd658cb7d',
        client_secret: '292f1925b829dae879fb651b8eddd932c3326c91',
    },
});
gitment.render('gitmentContainer');
</script>
