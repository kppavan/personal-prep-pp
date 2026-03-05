## Differrent Stages in Plugin execution pipeline

1. Pre-validation | 10 | Before Security check and data transaction

2. Pre-operation | 20 | Inside DB transaction before main operation

3. Main-operation | 30 | Conre platform transaction (cannot register custom plugin)

4. Post-operatoin | 40 | After main operation inside transaction if sync or outside if async
