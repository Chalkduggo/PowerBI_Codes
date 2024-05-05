C_CardTotal_Minutes_Viewed = 
VAR Minutes_Viewed = SUM('Combined OTT'[Minutes Viewed])
VAR Minutes_Viewed_MOM = [% MOM Minutes Viewed]

VAR Formatted_Min_Viewed =
    IF(Minutes_Viewed >= 1000000000,
        FORMAT(Minutes_Viewed / 1000000000, "0.00") & "Bn",
        IF(Minutes_Viewed >= 1000000,
            FORMAT(Minutes_Viewed / 1000000, "0.00") & "Mn",
            IF(Minutes_Viewed >= 1000,
                FORMAT(Minutes_Viewed / 1000, "0.00") & "K",
                FORMAT(Minutes_Viewed, "0"))))


VAR Arrow =
    IF(Minutes_Viewed_MOM > 0, UNICHAR(9650), IF(Minutes_Viewed_MOM < 0, UNICHAR(128315), ""))

RETURN
    Formatted_Min_Viewed & " " & " || % MOM : " & FORMAT(Minutes_Viewed_MOM, "0.00%") & Arrow
