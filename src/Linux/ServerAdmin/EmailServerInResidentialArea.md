If you are reading this, you have an extra PC, NAS, or raspberry pi that you are looking to make into a email server. Unfortunatelly, email servers are notoriously difficult to create. Fortunately enough, scripts have been created that more or less automate this process and stream lined a lot of it. Particularly, I nabbed a script off [Luke Smith](lukesmith.xyz) that installs and configures it for you. Unfortunately (again), if you are setting this server up in a residential area with residential email service you may have some difficulties outside of setting up the email server battling with your ISP (Internet Service Provider) due to blocked ports. Fortunately (again), there is a simple work around.

Conceptually there is not that much to do, which is what this blog post is going to be about. The specifics will be left to the script, so if you are interested in learning how that works go read through that. It isn't earth shattering, but there are enough intricies that I am going to stick to borrowing the script when needed. What it boils down to is: install postfix, install dovecot, install spamassasin, install OpenDKIM, configure postfix to utilize SMTP, configure dovecot to connect to postfix and allow external connection for IMAP, link spamassasin, and hook up OpenDKIM. If you didn't get all that, don't worry. Each section will break down the components.

The issue I came accross while setting up my email server is that my ISP (Internet Service Provider) was blocking port 25. Although I had a working email server, it was rendered useless because I couldn't send/receive email outside of my local network. This just requires some external help and minor tweaks on your end to get things moving smoothly. 

I'll also preface this by saying that the script README says that it is configured for VPS (Vitual Private Servers), but it worked great on my Debian 10 install on my 300$ little hp pavillion makeshift server. Now to talk about each component.

# Postfix

# Dovecot

# Spamassasin

# OpenDKIM
