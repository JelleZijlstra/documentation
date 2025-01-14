# settings

This request takes no additional request parameters other than the standard ones.

The server should respond with a response code of 200 and content type of `application/json`. The JSON response should be a dictionary containing the keys listed below. All keys are optional; if they are not specified the default values are used. Poe reserves the right to change the defaults at any time, so if bots rely on a particular setting, they should set it explicitly.

If a settings request fails (it does not return a 200 response code with a valid JSON body), the previous settings are used for the bot. If this is the first request, that means the default values are used for all settings; if it is a refetch request, the settings previously used for the bot remain in use. If the request does not return a 2xx or 501 response code, the Poe server may retry the settings request after some time.

### Response&#x20;

The response may contain the following keys:

* `context_clear_window_secs` (integer or null): If the user does not talk to the bot for this many seconds, we clear the context and start a fresh conversation. Future `query` requests will use a new conversation identifier and will not include previous messages in the prompt. For example, suppose this parameter is set to 1800 (30 \* 60), and a user sends a message to a bot at 1 pm. If they then send another message at 1:20 pm, the query send to the bot server will include the previous message and response, but if they send a third message at 2 pm, the query will include only the new message. If this parameter is set to 0, the context window is never cleared automatically, regardless of how long it has been since the user talked to the bot. If the parameter is omitted or `null`, the value will be determined by the Poe server.
* `allow_user_context_clear` (boolean): If true, allow users to directly clear their context window, meaning that their conversation with this bot will reset to a clean slate. This is independent from whether Poe itself will automatically clear context after a certain time (as controlled by `context_clear_window_secs`). The default is true.

