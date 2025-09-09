# ha-whodid

Get userid from context objects, even if the context itself does not have a userid provided.

## How it works
After creating the WhoDid instance, all events will be monitored. \
If a event context contains a userid, the context id will be used as a key and the user stored. \
Automations will provide a parent id field in the context obeject, which ties the context of the automation back to the event, that triggered the automation in the first place.

All integrations using this package will share a single instance. \
This is done to save memory.

## Example code
```
from hawhodid import WhoDid

  async def handle_servicecall(call: ServiceCall):
      whodidInstance = WhoDid(hass=call.hass)

      userid = await whodidInstance.getUserId(context=call.context)

      if userid == None:
          return
```

This best to put `WhoDid(hass=hass)` into the `setup` or `async_setup` function of your integration to ensure that all events from the beginning are accounted for.

## Work in progress
This is a bare bones implementation, that i made for my own integrations. \
I only made this to prevent code duplication and reduce memory usage. \
If you need something for you or any bugs, just create an issue or provide a solution with a PR. \
Both are appreciated.
