# Python Telegram Bot 
## Basic Ideas

[Wiki](https://github.com/python-telegram-bot/python-telegram-bot/wiki/)

A basic bot setup looks like this:

``` python
from telegram import Update
from telegram.ext import ApplicationBuilder, ContextTypes, CommandHandler

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await context.bot.send_message(chat_id=update.effective_chat.id, text="Hi!")


application = ApplicationBuilder().token('TOKEN').build()

start_handler = CommandHandler('start', start)
application.add_handler(start_handler)

application.run_polling()  
```  




## telegram.Update
`telegram.Update` objects contain data passed directly from the Telegram API after some event occurred.
 >_class_ telegram.Update(_update_id_, _message=None_, _edited_message=None_, _channel_post=None_, _edited_channel_post=None_, _inline_query=None_, _chosen_inline_result=None_, _callback_query=None_, _shipping_query=None_, _pre_checkout_query=None_, _poll=None_, _poll_answer=None_, _my_chat_member=None_, _chat_member=None_, _chat_join_request=None_, _chat_boost=None_, _removed_chat_boost=None_, _message_reaction=None_, _message_reaction_count=None_, _business_connection=None_, _business_message=None_, _edited_business_message=None_, _deleted_business_messages=None_, _purchased_paid_media=None_, _*_, _api_kwargs=None_)

Bases: [`telegram.TelegramObject`](https://docs.python-telegram-bot.org/en/v21.6/telegram.telegramobject.html#telegram.TelegramObject "telegram.TelegramObject")

This object represents an incoming update.

Objects of this class are comparable in terms of equality. Two objects of this class are considered equal, if their [`update_id`](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.update_id "telegram.Update.update_id") is equal.

> [!Note] 
> At most one of the optional parameters can be present in any given update.

Parameters:

- [**update_id**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.update_id) ([`int`](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)")) – The update’s unique identifier. Update identifiers start from a certain positive number and increase sequentially. If there are no new updates for at least a week, then identifier of the next update will be chosen randomly instead of sequentially.
    
- [**message**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.message) ([`telegram.Message`](https://docs.python-telegram-bot.org/en/v21.6/telegram.message.html#telegram.Message "telegram.Message"), optional) – New incoming message of any kind - text, photo, sticker, etc.
    
- [**edited_message**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.edited_message) ([`telegram.Message`](https://docs.python-telegram-bot.org/en/v21.6/telegram.message.html#telegram.Message "telegram.Message"), optional) – New version of a message that is known to the bot and was edited. This update may at times be triggered by changes to message fields that are either unavailable or not actively used by your bot.
    
- [**inline_query**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.inline_query) ([`telegram.InlineQuery`](https://docs.python-telegram-bot.org/en/v21.6/telegram.inlinequery.html#telegram.InlineQuery "telegram.InlineQuery"), optional) – New incoming inline query.
    
- [**chosen_inline_result**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.chosen_inline_result) ([`telegram.ChosenInlineResult`](https://docs.python-telegram-bot.org/en/v21.6/telegram.choseninlineresult.html#telegram.ChosenInlineResult "telegram.ChosenInlineResult"), optional) – The result of an inline query that was chosen by a user and sent to their chat partner.
    
- [**callback_query**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.callback_query) ([`telegram.CallbackQuery`](https://docs.python-telegram-bot.org/en/v21.6/telegram.callbackquery.html#telegram.CallbackQuery "telegram.CallbackQuery"), optional) – New incoming callback query.
    
- [**poll**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.poll) ([`telegram.Poll`](https://docs.python-telegram-bot.org/en/v21.6/telegram.poll.html#telegram.Poll "telegram.Poll"), optional) – New poll state. Bots receive only updates about manually stopped polls and polls, which are sent by the bot.
    
- [**poll_answer**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.poll_answer) ([`telegram.PollAnswer`](https://docs.python-telegram-bot.org/en/v21.6/telegram.pollanswer.html#telegram.PollAnswer "telegram.PollAnswer"), optional) – A user changed their answer in a non-anonymous poll. Bots receive new votes only in polls that were sent by the bot itself.
    
- [**my_chat_member**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.my_chat_member) ([`telegram.ChatMemberUpdated`](https://docs.python-telegram-bot.org/en/v21.6/telegram.chatmemberupdated.html#telegram.ChatMemberUpdated "telegram.ChatMemberUpdated"), optional) –
    
    The bot’s chat member status was updated in a chat. For private chats, this update is received only when the bot is blocked or unblocked by the user.
    
    Added in version 13.4.
    
- [**chat_member**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.chat_member) ([`telegram.ChatMemberUpdated`](https://docs.python-telegram-bot.org/en/v21.6/telegram.chatmemberupdated.html#telegram.ChatMemberUpdated "telegram.ChatMemberUpdated"), optional) –
    
    A chat member’s status was updated in a chat. The bot must be an administrator in the chat and must explicitly specify [`CHAT_MEMBER`](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.CHAT_MEMBER "telegram.Update.CHAT_MEMBER") in the list of [`telegram.ext.Application.run_polling.allowed_updates`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_polling.params.allowed_updates "telegram.ext.Application.run_polling") to receive these updates (see [`telegram.Bot.get_updates()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.bot.html#telegram.Bot.get_updates "telegram.Bot.get_updates"), [`telegram.Bot.set_webhook()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.bot.html#telegram.Bot.set_webhook "telegram.Bot.set_webhook"), [`telegram.ext.Application.run_polling()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_polling "telegram.ext.Application.run_polling") and [`telegram.ext.Application.run_webhook()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_webhook "telegram.ext.Application.run_webhook")).
    
    Added in version 13.4.
    
- [**chat_join_request**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.chat_join_request) ([`telegram.ChatJoinRequest`](https://docs.python-telegram-bot.org/en/v21.6/telegram.chatjoinrequest.html#telegram.ChatJoinRequest "telegram.ChatJoinRequest"), optional) –
    
    A request to join the chat has been sent. The bot must have the [`telegram.ChatPermissions.can_invite_users`](https://docs.python-telegram-bot.org/en/v21.6/telegram.chatpermissions.html#telegram.ChatPermissions.can_invite_users "telegram.ChatPermissions.can_invite_users") administrator right in the chat to receive these updates.
    
    Added in version 13.8.
    
    
- [**message_reaction**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.message_reaction) ([`telegram.MessageReactionUpdated`](https://docs.python-telegram-bot.org/en/v21.6/telegram.messagereactionupdated.html#telegram.MessageReactionUpdated "telegram.MessageReactionUpdated"), optional) –
    
    A reaction to a message was changed by a user. The bot must be an administrator in the chat and must explicitly specify [`MESSAGE_REACTION`](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.MESSAGE_REACTION "telegram.Update.MESSAGE_REACTION") in the list of [`telegram.ext.Application.run_polling.allowed_updates`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_polling.params.allowed_updates "telegram.ext.Application.run_polling") to receive these updates (see [`telegram.Bot.get_updates()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.bot.html#telegram.Bot.get_updates "telegram.Bot.get_updates"), [`telegram.Bot.set_webhook()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.bot.html#telegram.Bot.set_webhook "telegram.Bot.set_webhook"), [`telegram.ext.Application.run_polling()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_polling "telegram.ext.Application.run_polling") and [`telegram.ext.Application.run_webhook()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_webhook "telegram.ext.Application.run_webhook")). The update isn’t received for reactions set by bots.
    
    Added in version 20.8.
    
- [**message_reaction_count**](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.params.message_reaction_count) ([`telegram.MessageReactionCountUpdated`](https://docs.python-telegram-bot.org/en/v21.6/telegram.messagereactioncountupdated.html#telegram.MessageReactionCountUpdated "telegram.MessageReactionCountUpdated"), optional) –
    
    Reactions to a message with anonymous reactions were changed. The bot must be an administrator in the chat and must explicitly specify [`MESSAGE_REACTION_COUNT`](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update.MESSAGE_REACTION_COUNT "telegram.Update.MESSAGE_REACTION_COUNT") in the list of [`telegram.ext.Application.run_polling.allowed_updates`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_polling.params.allowed_updates "telegram.ext.Application.run_polling") to receive these updates (see [`telegram.Bot.get_updates()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.bot.html#telegram.Bot.get_updates "telegram.Bot.get_updates"), [`telegram.Bot.set_webhook()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.bot.html#telegram.Bot.set_webhook "telegram.Bot.set_webhook"), [`telegram.ext.Application.run_polling()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_polling "telegram.ext.Application.run_polling") and [`telegram.ext.Application.run_webhook()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.run_webhook "telegram.ext.Application.run_webhook")). The updates are grouped and can be sent with delay up to a few minutes.
    
    Added in version 20.8.
    


## telegram.ext.CallbackContext
### [CallbackContext](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#callbackcontext "Link to this heading")

> _class_ telegram.ext.CallbackContext(_application_, _chat_id=None_, _user_id=None_)[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L57-L441)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "Link to this definition")

This is a context object passed to the callback called by [`telegram.ext.BaseHandler`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.basehandler.html#telegram.ext.BaseHandler "telegram.ext.BaseHandler") or by the [`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application") in an error handler added by [`telegram.ext.Application.add_error_handler`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.add_error_handler "telegram.ext.Application.add_error_handler") or to the callback of a [`telegram.ext.Job`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.job.html#telegram.ext.Job "telegram.ext.Job").

Note

[`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application") will create a single context for an entire update. This means that if you got 2 handlers in different groups and they both get called, they will receive the same [`CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext") object (of course with proper attributes like [`matches`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.matches "telegram.ext.CallbackContext.matches") differing). This allows you to add custom attributes in a lower handler group callback, and then subsequently access those attributes in a higher handler group callback. Note that the attributes on [`CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext") might change in the future, so make sure to use a fairly unique name for the attributes.

Warning

Do not combine custom attributes with [`telegram.ext.BaseHandler.block`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.basehandler.html#telegram.ext.BaseHandler.params.block "telegram.ext.BaseHandler") set to [`False`](https://docs.python.org/3/library/constants.html#False "(in Python v3.12)") or [`telegram.ext.Application.concurrent_updates`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.concurrent_updates "telegram.ext.Application.concurrent_updates") set to [`True`](https://docs.python.org/3/library/constants.html#True "(in Python v3.12)"). Due to how those work, it will almost certainly execute the callbacks for an update out of order, and the attributes that you think you added will not be present.



Parameters:

- [**application**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.params.application) ([`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application")) – The application associated with this context.
- [**chat_id**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.params.chat_id) ([`int`](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"), optional) –
    The ID of the chat associated with this object. Used to provide [`chat_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.chat_data "telegram.ext.CallbackContext.chat_data").
- [**user_id**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.params.user_id) ([`int`](https://docs.python.org/3/library/functions.html#int "(in Python v3.12)"), optional) –    
    The ID of the user associated with this object. Used to provide [`user_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.user_data "telegram.ext.CallbackContext.user_data").

Attributes:

`coroutine`
Optional. Only present in error handlers if the error was caused by an awaitable run with [`Application.create_task()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.create_task "telegram.ext.Application.create_task") or a handler callback with [`block=False`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.basehandler.html#telegram.ext.BaseHandler.block "telegram.ext.BaseHandler.block").
Type:
[awaitable](https://docs.python.org/3/glossary.html#term-awaitable "(in Python v3.12)")

`matches`
Optional. If the associated update originated from a [`filters.Regex`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.filters.html#telegram.ext.filters.Regex "telegram.ext.filters.Regex"), this will contain a list of match objects for every pattern where `re.search(pattern, string)` returned a match. Note that filters short circuit, so combined regex filters will not always be evaluated.
Type:

List\[[re.Match](https://docs.python.org/3/library/re.html#re.Match.expand)\]

`args`

Optional. Arguments passed to a command if the associated update is handled by [`telegram.ext.CommandHandler`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.commandhandler.html#telegram.ext.CommandHandler "telegram.ext.CommandHandler"), [`telegram.ext.PrefixHandler`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.prefixhandler.html#telegram.ext.PrefixHandler "telegram.ext.PrefixHandler") or [`telegram.ext.StringCommandHandler`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.stringcommandhandler.html#telegram.ext.StringCommandHandler "telegram.ext.StringCommandHandler"). It contains a list of the words in the text after the command, using any whitespace string as a delimiter.

Type:
List\[str\]

error[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L139-L155)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.error "Link to this definition")

Optional. The error that was raised. Only present when passed to an error handler registered with [`telegram.ext.Application.add_error_handler`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.add_error_handler "telegram.ext.Application.add_error_handler").

Type:

[`Exception`](https://docs.python.org/3/library/exceptions.html#Exception "(in Python v3.12)")

job[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L139-L155)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.job "Link to this definition")

Optional. The job which originated this callback. Only present when passed to the callback of [`telegram.ext.Job`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.job.html#telegram.ext.Job "telegram.ext.Job") or in error handlers if the error is caused by a job.

Changed in version 20.0: [`job`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.job "telegram.ext.CallbackContext.job") is now also present in error handlers if the error is caused by a job.

Type:

[`telegram.ext.Job`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.job.html#telegram.ext.Job "telegram.ext.Job")

_property_ application[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L156-L160)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.application "Link to this definition")

The application associated with this context.

Type:

[`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application")

_property_ bot[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L399-L403)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.bot "Link to this definition")

The bot associated with this context.

Type:

[`telegram.Bot`](https://docs.python-telegram-bot.org/en/v21.6/telegram.bot.html#telegram.Bot "telegram.Bot")

_property_ bot_data[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L161-L170)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.bot_data "Link to this definition")

Optional. An object that can be used to keep any data in. For each update it will be the same [`ContextTypes.bot_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.contexttypes.html#telegram.ext.ContextTypes.bot_data "telegram.ext.ContextTypes.bot_data"). Defaults to [`dict`](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)").

See also

[Storing Bot, User and Chat Related Data](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Storing-bot%2C-user-and-chat-related-data)

Type:

[`ContextTypes.bot_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.contexttypes.html#telegram.ext.ContextTypes.bot_data "telegram.ext.ContextTypes.bot_data")

_property_ chat_data[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L177-L197)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.chat_data "Link to this definition")

Optional. An object that can be used to keep any data in. For each update from the same chat id it will be the same [`ContextTypes.chat_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.contexttypes.html#telegram.ext.ContextTypes.chat_data "telegram.ext.ContextTypes.chat_data"). Defaults to [`dict`](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)").

Warning

When a group chat migrates to a supergroup, its chat id will change and the `chat_data` needs to be transferred. For details see our [wiki page](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Storing-bot,-user-and-chat-related-data#chat-migration).

See also

[Storing Bot, User and Chat Related Data](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Storing-bot%2C-user-and-chat-related-data)

Changed in version 20.0: The chat data is now also present in error handlers if the error is caused by a job.

Type:

[`ContextTypes.chat_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.contexttypes.html#telegram.ext.ContextTypes.chat_data "telegram.ext.ContextTypes.chat_data")

drop_callback_data(_callback_query_)[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L252-L282)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.drop_callback_data "Link to this definition")

Deletes the cached data for the specified callback query.

Added in version 13.6.

Note

Will _not_ raise exceptions in case the data is not found in the cache. _Will_ raise [`KeyError`](https://docs.python.org/3/library/exceptions.html#KeyError "(in Python v3.12)") in case the callback query can not be found in the cache.

See also

[Arbitrary callback_data](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Arbitrary-callback_data)

Parameters:

[**callback_query**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.drop_callback_data.params.callback_query) ([`telegram.CallbackQuery`](https://docs.python-telegram-bot.org/en/v21.6/telegram.callbackquery.html#telegram.CallbackQuery "telegram.CallbackQuery")) – The callback query.

Raises:

[**KeyError**](https://docs.python.org/3/library/exceptions.html#KeyError "(in Python v3.12)") **|** [**RuntimeError**](https://docs.python.org/3/library/exceptions.html#RuntimeError "(in Python v3.12)") – [`KeyError`](https://docs.python.org/3/library/exceptions.html#KeyError "(in Python v3.12)"), if the callback query can not be found in the cache and [`RuntimeError`](https://docs.python.org/3/library/exceptions.html#RuntimeError "(in Python v3.12)"), if the bot doesn’t allow for arbitrary callback data.

_classmethod_ from_error(_update_, _error_, _application_, _job=None_, _coroutine=None_)[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L283-L335)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_error "Link to this definition")

Constructs an instance of [`telegram.ext.CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext") to be passed to the error handlers.

See also

[`telegram.ext.Application.add_error_handler()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.add_error_handler "telegram.ext.Application.add_error_handler")

Changed in version 20.0: Removed arguments `async_args` and `async_kwargs`.

Parameters:

- [**update**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_error.params.update) ([`object`](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)") | [`telegram.Update`](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update "telegram.Update")) – The update associated with the error. May be [`None`](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)"), e.g. for errors in job callbacks.
    
- [**error**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_error.params.error) ([`Exception`](https://docs.python.org/3/library/exceptions.html#Exception "(in Python v3.12)")) – The error.
    
- [**application**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_error.params.application) ([`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application")) – The application associated with this context.
    
- [**job**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_error.params.job) ([`telegram.ext.Job`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.job.html#telegram.ext.Job "telegram.ext.Job"), optional) –
    
    The job associated with the error.
    
    Added in version 20.0.
    
- [**coroutine**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_error.params.coroutine) ([awaitable](https://docs.python.org/3/glossary.html#term-awaitable "(in Python v3.12)"), optional) –
    
    The awaitable associated with this error if the error was caused by a coroutine run with [`Application.create_task()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.create_task "telegram.ext.Application.create_task") or a handler callback with [`block=False`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.basehandler.html#telegram.ext.BaseHandler.block "telegram.ext.BaseHandler.block").
    
    Added in version 20.0.
    
    Changed in version 20.2: Accepts [`asyncio.Future`](https://docs.python.org/3/library/asyncio-future.html#asyncio.Future "(in Python v3.12)") and generator-based coroutine functions.
    

Returns:

[`telegram.ext.CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext")

_classmethod_ from_job(_job_, _application_)[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L366-L389)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_job "Link to this definition")

Constructs an instance of [`telegram.ext.CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext") to be passed to a job callback.

See also

[`telegram.ext.JobQueue()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.jobqueue.html#telegram.ext.JobQueue "telegram.ext.JobQueue")

Parameters:

- [**job**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_job.params.job) ([`telegram.ext.Job`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.job.html#telegram.ext.Job "telegram.ext.Job")) – The job.
    
- [**application**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_job.params.application) ([`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application")) – The application associated with this context.
    

Returns:

[`telegram.ext.CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext")

_classmethod_ from_update(_update_, _application_)[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L336-L365)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_update "Link to this definition")

Constructs an instance of [`telegram.ext.CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext") to be passed to the handlers.

See also

[`telegram.ext.Application.add_handler()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.add_handler "telegram.ext.Application.add_handler")

Parameters:

- [**update**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_update.params.update) ([`object`](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)") | [`telegram.Update`](https://docs.python-telegram-bot.org/en/v21.6/telegram.update.html#telegram.Update "telegram.Update")) – The update.
    
- [**application**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.from_update.params.application) ([`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application")) – The application associated with this context.
    

Returns:

[`telegram.ext.CallbackContext`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext "telegram.ext.CallbackContext")

_property_ job_queue[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L404-L419)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.job_queue "Link to this definition")

The [`JobQueue`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.jobqueue.html#telegram.ext.JobQueue "telegram.ext.JobQueue") used by the [`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application").

See also

[Job Queue](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Extensions---JobQueue)

Type:

[`telegram.ext.JobQueue`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.jobqueue.html#telegram.ext.JobQueue "telegram.ext.JobQueue")

_property_ match[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L430-L441)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.match "Link to this definition")

The first match from [`matches`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.matches "telegram.ext.CallbackContext.matches"). Useful if you are only filtering using a single regex filter. Returns [`None`](https://docs.python.org/3/library/constants.html#None "(in Python v3.12)") if [`matches`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.matches "telegram.ext.CallbackContext.matches") is empty.

Type:

[`re.Match`](https://docs.python.org/3/library/re.html#re.Match.expand "(in Python v3.12)")

_async_ refresh_data()[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L226-L251)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.refresh_data "Link to this definition")

If [`application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.application "telegram.ext.CallbackContext.application") uses persistence, calls [`telegram.ext.BasePersistence.refresh_bot_data()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.basepersistence.html#telegram.ext.BasePersistence.refresh_bot_data "telegram.ext.BasePersistence.refresh_bot_data") on [`bot_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.bot_data "telegram.ext.CallbackContext.bot_data"), [`telegram.ext.BasePersistence.refresh_chat_data()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.basepersistence.html#telegram.ext.BasePersistence.refresh_chat_data "telegram.ext.BasePersistence.refresh_chat_data") on [`chat_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.chat_data "telegram.ext.CallbackContext.chat_data") and [`telegram.ext.BasePersistence.refresh_user_data()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.basepersistence.html#telegram.ext.BasePersistence.refresh_user_data "telegram.ext.BasePersistence.refresh_user_data") on [`user_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.user_data "telegram.ext.CallbackContext.user_data"), if appropriate.

Will be called by [`telegram.ext.Application.process_update()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application.process_update "telegram.ext.Application.process_update") and [`telegram.ext.Job.run()`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.job.html#telegram.ext.Job.run "telegram.ext.Job.run").

Added in version 13.6.

update(_data_)[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L390-L398)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.update "Link to this definition")

Updates `self.__slots__` with the passed data.

Parameters:

[**data**](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.update.params.data) (Dict[[`str`](https://docs.python.org/3/library/stdtypes.html#str "(in Python v3.12)"), [`object`](https://docs.python.org/3/library/functions.html#object "(in Python v3.12)")]) – The data.

_property_ update_queue[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L420-L429)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.update_queue "Link to this definition")

The [`asyncio.Queue`](https://docs.python.org/3/library/asyncio-queue.html#asyncio.Queue "(in Python v3.12)") instance used by the [`telegram.ext.Application`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.application.html#telegram.ext.Application "telegram.ext.Application") and (usually) the [`telegram.ext.Updater`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.updater.html#telegram.ext.Updater "telegram.ext.Updater") associated with this context.

Type:

[`asyncio.Queue`](https://docs.python.org/3/library/asyncio-queue.html#asyncio.Queue "(in Python v3.12)")

_property_ user_data[[source]](https://github.com/python-telegram-bot/python-telegram-bot/blob/v21.6/telegram/ext/_callbackcontext.py#L204-L219)[](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.callbackcontext.html#telegram.ext.CallbackContext.user_data "Link to this definition")

Optional. An object that can be used to keep any data in. For each update from the same user it will be the same [`ContextTypes.user_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.contexttypes.html#telegram.ext.ContextTypes.user_data "telegram.ext.ContextTypes.user_data"). Defaults to [`dict`](https://docs.python.org/3/library/stdtypes.html#dict "(in Python v3.12)").

See also

[Storing Bot, User and Chat Related Data](https://github.com/python-telegram-bot/python-telegram-bot/wiki/Storing-bot%2C-user-and-chat-related-data)

Changed in version 20.0: The user data is now also present in error handlers if the error is caused by a job.

Type:

[`ContextTypes.user_data`](https://docs.python-telegram-bot.org/en/v21.6/telegram.ext.contexttypes.html#telegram.ext.ContextTypes.user_data "telegram.ext.ContextTypes.user_data")