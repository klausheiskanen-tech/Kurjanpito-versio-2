[README.md](https://github.com/user-attachments/files/26698507/README.md)
# Kirjanpito-ohjelma versio 2

Pienyritykselle suunniteltu kirjanpito-ohjelma, joka toimii selaimessa.

## Ominaisuudet

- **Tositteiden kirjaus** — myyntilaskut, ostolaskut, palkka, maksut ja vapaat kirjaukset
- **Palkanlaskenta** — bruttopalkka lasketaan automaattisesti nettopalkasta verokortin tietojen perusteella
- **Palkkakuitti** — tulostettava palkkalaskelma työntekijälle
- **Verojen tilitys** — erillinen kirjaus ennakonpidätyksen ja sotumaksun tilityksestä OmaVeroon
- **Tuloslaskelma** — tuotot ja kulut valitulta ajanjaksolta
- **Tase** — vastaavaa ja vastattavaa
- **ALV-laskelma** — arvonlisäveron seuranta
- **Liitetiedostot** — kuittien ja laskujen liittäminen tositteisiin (PDF, PNG, JPG)
- **Asetukset** — yritys- ja työntekijätiedot
- **Verokortti** — veroprosenttien hallinta
- **Käyttäjätunnistus** — kirjautuminen salasanalla

## Teknologiat

- Python 3
- Flask + Flask-Login
- SQLite
- Jinja2-templatet

## Asennus

1. Kloonaa repo:
   ```bash
   git clone https://github.com/klausheiskanen-tech/Kurjanpito-versio-2.git
   cd Kurjanpito-versio-2
   ```

2. Asenna riippuvuudet:
   ```bash
   pip install flask flask-login werkzeug
   ```

3. Käynnistä sovellus:
   ```bash
   python app.py
   ```

4. Avaa selaimessa: `http://localhost:5000`

## Tietokanta

Ohjelma luo automaattisesti `kirjanpito.db` SQLite-tietokannan ensimmäisellä käynnistyskerralla.

## Kirjanpitologiikka

**Palkanmaksu kirjataan kahdessa vaiheessa:**

1. Palkanlaskenta:
   - 5010 Kuukausipalkat (debet) = bruttopalkka
   - 2921 Ennakonpidätysvelka (kredit) = ennakonpidätys
   - 2923 Sosiaaliturvamaksuvelka (kredit) = sotumaksu
   - 1910 Pankki (kredit) = nettopalkka

2. Verojen tilitys OmaVeroon:
   - 2921 Ennakonpidätysvelka (debet)
   - 2923 Sosiaaliturvamaksuvelka (debet)
   - 1910 Pankki (kredit)
