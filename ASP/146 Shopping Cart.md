

## Errors
#### Get Basket
Now, we can add item into a basket. It returns the buyer ID and other things. But, it seems nothings go into cookies.
So, when we send a request for getting the basket. It returns Not Found.

Someone says Axois does not use cookies by default. We can set `axios.default.withCredentials = true;` for it.

Solved by `var cookieOptions = new CookieOptions { IsEssential = true, Expires = DateTime.Now.AddDays(10), SameSite=SameSiteMode.None, Secure=true };` in Asp.net Core. We need `SameSite & Secure`.