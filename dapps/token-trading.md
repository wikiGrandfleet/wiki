<!-- TITLE: Token Trading -->
<!-- SUBTITLE: A quick summary of Token Trading -->

### July 1 2018

#### Debugging web pack issues

At some point I had deleted the `index.html` that webpack injected into, as a result my code did not compile, only when I turned debug: quiet, to false could I see the necessary messages.

In general, I prefer to have a lot of error messages, but given the nature of my mistake, it makes sense that I got an general error message (deleting a file).

I decided to use vuetify (front-end component library for vue), cause this looks amazing.

In addition, changing the login form requires a lot of though, I could set up a system in which only registered users via smart contract as access permitted routes, but first I'll build out some contracts.

#### Updating npm packages for vue 
Killing existing chromedriver processes, when I was trying to update vue to 2.5.0 for compatability with vuetify, I keep getting error messages indicated 
```sh
Clear-Host 
Get-Process chromedriver | Stop-Process
``