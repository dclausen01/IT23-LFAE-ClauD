`UPDATE RP 
`SET RP.RgPos_RabattProzent = 12` 
`FROM RechnungPosition RP 
`JOIN Rechnung R ON RP.RgPos_RgIdKey = R.Rg_IdKey 
`JOIN Artikel A ON RP.RgPos_ArtIdKey = A.Art_IdKey 
`WHERE R.Rg_Datum like '2023%' AND A.Art_WaIdKey = 2 AND RP.RgPos_RabattProzent = 0`

