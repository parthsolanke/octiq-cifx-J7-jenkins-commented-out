# CI detection fixture

The only `npm test` is inside // and /* */ comments. Must NOT count.

Expected verdict line in the Octiq chat:

    anything EXCEPT 'Tests required' (expect 'Tests not required - ...')
