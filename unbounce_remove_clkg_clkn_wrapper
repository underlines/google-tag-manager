<script>
/* Unbounce clkg clkn link wrapper remover (vanilla js)
 * Unbounce uses a wrapper to modify all links on the landing page examplelandingpage.com from <a href='http://link.com/about'> to <a href='http://examplelandingpage.com/clkg/http/link.com/about'>
 * This script removes all clkg clkn wrappers from all http, https, tel and mailto links
*/ 2017-12-27 github.com/underlines

var links = document.getElementsByTagName('a');
for(var i = 0; i<links.length; i++){
    var link = links[i];
    if(link.hasAttribute('href')){                  // "https://www2.lpt.co.th/en/clkg/tel/020262127" "https://www2.lpt.co.th/en/clkg/https/www.zipeventapp.com/e/LPT-PP22-Buy-3-PLATINUM-get-1-PLATINUM?ref=HERO"
        var newLink = link.href
        .replace(/.*\/clk(g|n)\/https\//gi,'https://')
        .replace(/.*\/clk(g|n)\/http\//gi,'http://')
        .replace(/.*\/clk(g|n)\/tel\//gi,'tel:')
        .replace(/.*\/clk(g|n)\/mailto\//gi,'mailto:');
        link.href = newLink;
    }
}
</script>
