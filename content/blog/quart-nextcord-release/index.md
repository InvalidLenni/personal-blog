---
title: "Quart-Nextcord RELEASE"
date: "2022-06-04T07:04:15.00Z" 
description: "Quart-Nextcord is a Discord OAuth2 extension for Quart using nextcord."

---

# Quart-Nextcord - Discord OAuth2 extension for Quart using nextcord.

Quart-Nextcord is an extension for [nextcord](https://pypi.org/project/nextcord).


## Related links
- [Quart-Nextcord PyPi](https://pypi.org/project/Quart-Nextcord)
- [Quart-Nextcord GitHub Repository](https://github.com/InvalidLenni/Quart-Nextcord)
- [Quart-Nextcord Documentation](https://quart-nextcord.rtfd.io)

## Example
 ```python 
 from quart import Quart, redirect, url_for 
 from quart_nextcord import DiscordOAuth2Session, requires_authorization, Unauthorized 
  
 app = Quart(__name__) 
  
 app.secret_key = b"random bytes representing quart secret key" 
  
 app.config["DISCORD_CLIENT_ID"] = 490732332240863233  # Discord client ID. 
 app.config["DISCORD_CLIENT_SECRET"] = ""  # Discord client secret. 
 app.config["DISCORD_REDIRECT_URI"] = ""  # URL to your callback endpoint. 
 app.config["DISCORD_BOT_TOKEN"] = ""  # Required to access BOT resources. 
  
 nextcord = DiscordOAuth2Session(app) 
  
  
 @app.route("/login/") 
 async def login(): 
     return await nextcord.create_session() 
  
  
 @app.route("/callback/") 
 async def callback(): 
     await nextcord.callback() 
     return redirect(url_for(".me")) 
  
  
 @app.errorhandler(Unauthorized) 
 async def redirect_unauthorized(e): 
     return redirect(url_for("login")) 
  
  
 @app.route("/me/") 
 @requires_authorization 
 async def me(): 
     user = await nextcord.fetch_user() 
     return f""" 
     <html> 
         <head> 
             <title>{user.name}</title> 
         </head> 
         <body> 
             <img src='{user.avatar_url}' /> 
         </body> 
     </html>""" 
  
  
 if __name__ == "__main__": 
     app.run() 
 ```


# Ideas?
Go to https://github.com/InvalidLenni/Quart-Nextcord/discussions

# You found issues?
Go to https://github.com/InvalidLenni/Quart-Nextcord/issues/new


# Contribution
You can make contributions too for helping us! 😃
