# Plugin basics

## Differrent Stages in Plugin execution pipeline

1. Pre-validation | 10 | Before Security check and data transaction

2. Pre-operation | 20 | Inside DB transaction before main operation

3. Main-operation | 30 | Conre platform transaction (cannot register custom plugin)

4. Post-operatoin | 40 | After main operation inside transaction if sync or outside if async

## What happens in pre validation stage.

- Executes before security checks
- Executes outside database transaction
- Good place to:

1. Cancel operation early
2. Validate business rules
3. Throw custom exceptions

## What is Pre-operation stage.

- Executes inside dtabase transaction
- Before data is commited to DB
- Used to:

1. Modify target value
2. Set default value
3. Updated fields without extra updates

## What is Post-operation stage.

- Executes after record is saved.
- Inside transaction (sync)
- Outside transaction (async)
  \*used for:

1. Creating related records
2. Sending data to external systems
3. Logging
4. Triggering workflows.

## Main operation plugin cannot be registered as it is a core platform operation.

## Throwing exception in different stages of plugin.

- Pre Validation -> Operation stops, no transaction started
- Pre Operation -> Entire transaction rolls back
- Post Operation (sync)-> transaction rolls back
- Post Operation (async) -> Record already saved only the async job fails

## Sync and Async Plugin

- sync

1. runs immediately
2. user waits
3. can rollback transaction
4. Real time validation

- Async

1. runs in the background
2. user does not wait
3. Cannot rollback main operation
4. External integrations

## Depth in plugin

## Context.Depth indicates how many times plugin is triggered in call stack.

Used to : Avoid infiite loop
`if (context.Depth > 1) return;`
