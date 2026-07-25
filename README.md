# Usporedba OSM shapefileova — nove zgrade

Javna web stranica (radi potpuno u pregledniku, bez servera) koja uspoređuje
dva shapefile snimka zgrada i prikazuje sve koje su nove u novijem snimku —
s adresom (ako postoji u podacima), svim OSM podacima, i filterima.

## Postavljanje na GitHub Pages

1. Kreiraj novi repozitorij na GitHubu (npr. `zagreb-usporedba`).
2. Pushaj ovu `index.html` datoteku u repozitorij (isti postupak kao kod
   `gradnja` repozitorija — `git init`, `git add .`, `git commit`, `git push`).
3. Settings → Pages → Source: `main` grana, `/ (root)` folder → Save.
4. Stranica će biti dostupna na `https://<korisničko-ime>.github.io/<naziv-repo>/`.
5. Ako je repozitorij privatan, GitHub Pages traži javnu vidljivost repozitorija
   (isto ograničenje na koje smo naišli i kod `gradnja` repozitorija) —
   Settings → General → Danger Zone → Change repository visibility → Public.

## Kako se koristi

1. Korisnik učita dva shapefile snimka, svaki zapakiran kao `.zip`
   (mora sadržavati `.shp`, `.shx`, `.dbf`, po mogućnosti `.prj`).
2. Alat automatski prepozna ID polje (traži `osm_id` ili slično), ali
   korisnik može ručno odabrati drugo polje ako je potrebno.
3. Klik na "Usporedi" — sve se radi lokalno u pregledniku (JavaScript
   biblioteka `shpjs` parsira shapefile direktno, bez slanja na server).
4. Ako neke nove zgrade nemaju upisanu adresu, alat automatski pokuša
   dohvatiti podatke o cestama (Overpass API) da izračuna najbližu
   imenovanu ulicu. Ako taj dohvat ne uspije (javni servis je nekad
   zauzet), korisniku se nudi ručni upload shapefilea cesta kao rezerva.
5. Rezultati se filtriraju po bilo kojem podatku (polju) koji postoji u
   učitanom shapefileu, s prekidačem I/ILI logike.

## Napomena o adresama

Standardni besplatni Geofabrik shapefile (`gis_osm_buildings_a_free_1`) NE
sadrži adresu — samo `osm_id`, `code`, `fclass`, `name`, `type`. Ako se
učita takav file, prikazivat će se samo najbliža ulica, ne stvarna adresa.
Za stvarne adrese treba izvor podataka koji uključuje `addr:street` /
`addr:housenumber` (npr. naša ranija ekstrakcija preko punog OSM exporta).

## Ograničenja

- Lista prikazuje do 500 rezultata odjednom (radi brzine u pregledniku) —
  suzite filterima/pretragom za više preciznosti.
- Automatski dohvat cesta ovisi o javnoj dostupnosti Overpass API-ja, koji
  znade biti privremeno preopterećen.
- Podudaranje ID-jeva pretpostavlja da oba shapefilea koriste isti sustav
  identifikatora (npr. oba iz OSM-a preko istog alata/verzije).
