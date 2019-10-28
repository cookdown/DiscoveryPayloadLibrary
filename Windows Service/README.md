These payloads are for the Squared Up EAM Library Management Pack from Squared Up. This MP monitors Windows Services and is used by VADA for discovering/monitoring Windows Services

# Important Note
Out of the box ServiceNow contains no Identification Rule/Entry for cmdb_ci_windows_service so you will need to manually create one for these payloads to work.
The class must be made dependant on Windows Server (cmdb_ci_win_server) and should identify on the "name" and "correlation_id" (or the field you store the CIs SCOM object ID in) fields 