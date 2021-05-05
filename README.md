# Základní dokumentace dotazníkového systému
## Základní nastavení dotazníku
### Dotazník
* **Name**
* **Title**
* **Author**
* **Test** - Dotazník je stále ve vývoji není pro koncového uživatele
* **Defaults** - defaultní hodnoty proměných
* **track** - informace které budeme o uživateli shromažďovat
* **Languages** - nastavení dostupných jazykových mutací
* **languageSources** - cesty k souborům s jazykovou mutací
* **Copyright** - nastavení textu zobrazeného ve footeru známeho jako copyright
* **saveProgress** - nastavení ukládání progresu při vyplňování dotazníku
  * “always” - postup dotazníku se ukládá
  * “log-only” - jednotlivé pokusy o vyplnění se ukládají do logu
  * “never” - nejde nic
* **resume** - načte uložený progres dotazníku, a otevře dotazník na zavřené stránce
* **prefill** - načte předchozí zadané hodnoty, když je resume true tak nedělá prefill nedělá nic
* **content** - list otázek
* **Id & uuid** - identifikátor dotazníku, změní se podle potřeby vaší databáze
* Použití

      name: "Ukázkový dotazník",
    	title: "Ukázkový dotazník 1",
    	author: "Jméno Přijmení",
    	test: true,
    	defaults: {
	    	"a": 3
	    },
    	track: [
   	  	"location",
	    	"ip",
	    	"camera"
    	],
	    languageShownAs: "flags",
	    "languages": [
	    	"cs-CZ",
	    	"en-US",
	    	"sk"
    	],
    	languageSources: [
	    	{
	    		"path": "/welcome.lang.ts"
	    	}
	    ],
	    copyright: "Sample Copyrightd",
	    saveProgress: "always",
	    resumeOnTheLastQuestion: false,
	    prefillValues: false,
      content: [
      
      ]



# Komponenty dotazníku
## Heading
* Jedná se o nadpis u každé jednotlivé otázky
* Parametry
  * **type** - používá se k určení komponenty
    * “heading”
    * “h”
  * **level** - určuje velikost nadpisu, může být i prázdný
    * “primary” nebo “1”
    * “secondary” nebo “2”
    * “tertiary” nebo “3”
  * **content** - samotný text nadpisu formát string
* Použití

      content: [
        { type: "heading", content: "Můžete dodat nějaký názor na reklamy během LOH?" }
      ]

## Paragraph
* Jedná se o text který se nachází pod nadpisem
* Parametry
  * **type** - používá se k určení komponenty
    * “paragraph”
    * “p”
  * **indent** - odsazení prvního řádku odstavce 
    * “Number” - uvádí se v pixelech
    * “String” - uvádí se jak hodnota tak jednotka odsazení
  * **Image** -
  * **Heading** -
  * **content** - obsah Paragrafu, formát string
* Použití


## Bulletpoint
* Jedná se o komponent bullet point viz. Obrázek
* Parametry
  * **type** - používá se k určení komponenty 
    * “bulletpoint”
    * “bullet”
    * “b”
  * **paragraphs** - 
    * string
    * IParagraph
  * **bullet** - nastaví obrazec bulletpointu
    * “circle”
    * “alpha”
    * “upper-roman”
    * “lower-roman”
    * “upper-alpha”
    * “lower-alpha”
    * IEmbeddedImage
* Použití


## TextField
* Jedná se o input typu textového pole
* Parametry
  * **type** - používá se k určení komponenty
    * “textfield”
    * “textbox”
    * “t”
  * **default** - placeholder zapsaný ve formátu string
  * **label** - label zapsaný ve formátu string (nadpis nad textovým polem)
  * **suggestions** - 
* Použití

      content: [
        { type: "textbox", label: "Váš názor:" }
      ]

## CheckBox
* Jedná se o checkbox nebo několik checkboxů
* Parametry
  * **type** - používá se k určení komponenty
    * “checkbox”
    * “c”
  * **content** - 
  * **shuffle** - 
  * **recordOrder** - 
  * **heading** - 
* Použití

      content: [{
					heading: "Jaké jsou vaše oblíbené sporty na LOH?",
					type: "checkbox",
					output: { value: "other" },
					content: ["Atletika", "Fotbal", "Plavecké sporty", "Politika", {label: "CTF", exclusive: true}, { label: "Nemám rád sporty", exclusive: true }]
			}]

## RadioButton
* Jedná se o skupinu radio buttonů
* Parametry
  * **type** - používá se k určení komponenty
    * “radiobutton”
    * “radio”
    * “r” 
  * **content** - 
  * **preset** - 
  * **default** - 
  * **shuffle** - 
  * **heading** -
* Použití

      content: [{
					heading: "O jaký sport se jedná?",
					type: "radio",
					content: ["Fotbal", "Judo", "Rugby", "Bojové sporty", "Golf", "Nevím"]
			}]

## ImageSelect
* Jedná se o výběr jednoho nebo více obrázků
* Parametry
  * **type** - použivá se k určení komponenty
    * “imageselect”
    * “is”
  * **content** - jedná se o list(pole) jednotlivých Obrázků
    * IImageSelectUnit
  * **radio** - pokud se nastaví true bude se chovat jako radio button a pujde vybrat pouze jeden
    * boolean - (true/false)
  * **shuffle** -
    * IShuffleParameters
    * IShuffleParameters[]
  * **heading** -
    * IHeading
    * string
* Použití

      content: [{
					span: 6,
					heading: "V jakém roce byla použita tato hudební ukázka jako hymna OH?",
					type: "imageselect",
					radio: true,
					output: { value: "test123" },
					content: [
						{ label: "1984", image: { url: "https://drwyjmricaxm7.cloudfront.net/repository/Seoul-Day-Tours-and-Activities--South-Korea--On-The-Go-Tours-435851504695803_crop_800_600.jpg" } },
						{ label: "2000", image: { url: "https://media2.s-nbcnews.com/j/newscms/2020_24/3387536/200611-seattle-autonomous-zone-al-1224_fa7ea9526005037ed63b4f95fa18d170.fit-760w.jpg" } },
						{ label: "2022", default: true, image: { url: "https://i1.wp.com/www.capitolhillseattle.com/wp-content/uploads/2020/06/CHSBLMJune92020-17.jpg" } }]
			}]

## Select
* Jedná se o combobox, s možností výběru jedné nebo více hodnot
* Parametry
  * **type** - používá se k určení komponenty
    * “selectbox”
    * “select”
    * “s”
  * **label** - jmenovka přiřazená k selectu
    * string
  * **size** - počet zobrazených řádků bez potřeby scrollovat
    * number
  * **radio** - pokud je true je možnost výběru více hodnot
    * boolean - (true/false)
  * **content** - pole objektu kde bude styl a obsah
    * ISelectUnit[]
    * string[]
  * **shuffle** -
    * IShuffleParameters
    * IShuffleParameters[]
* Použití

      content: [{
					type: "select",
					content: ["Televizní vysílání", "Doma", "V japonsku", "Nebudu sledovat"]
			}]

## Slider
* Jedná se o posuvný výběr
* Parametry
  * **type** - používá se k určení komponenty
    * “slider”
    * “sd”
  * **default** - základní hodnota
    * number
  * **min** - minimální hodnota
    * number
  * **max** - maximální hodnota
    * number
  * **step** - O kolik se bude slider posouvat
    * number
  * **design** - barva
    * string
  * **sliders** - počet sliderů
    * number
    * string[]
    * IEmbeddedText[]
  * **showGauge** - ukazování čísel při posunu
    * boolean - (true/false)
  * **rangeSlider** - jestli to bude úsekový slider (2 body)
    * boolean - (true/false)
    * IRangeSlider
  * **vertical** - zda bude slider vertikálně
    * boolean - (true/false)
* Použití

      content: [
				{ type: "heading", content: "Sledovali jste LOH s přáteli? Kdyžtak kolik vás bylo?" },
				{ type: "radio", default: 0, output: { value: "presne" }, content: [{ label: "Sám" }, "Znám přesný počet", "Přibližný počet"] },
				{ type: "slider", min: 0, max: 10, default: 5, sliders: ["Přesný počet:", "dalsi posuvnik"], if: "$presne == 1" },
				{ type: "slider", rangeSlider: { fromDefault: 4, toDefault: 6 }, min: 0, max: 10, sliders: ["Přibližný počet:"], if: "$presne == 2" }
			]

## Table
* Jedná se o tabulku naplněnou daty
* Parametry
  * **type** - používá se k určení komponenty
    * "table"
  * **rows** -
    * TableRow[]
  * **shuffleRows** -
    * IShuffleParameters
    * IShuffleParameters[]
  * **heading** -
    * IHeading
    * string
  * **darkEffect** - tmavé pozadí
    * boolean - (true/false)
  * **hoverEffect** - effekt při přejetí myšítkem přes buňku
    * boolean - (true/false)
* Použití

      content: [{ type: "heading", content: "Ohlas politických stran" }, {
				type: "table",
				rows: [
					{ head: true, columns: [{ head: true, content: "<b>Strana</b>" }, { content: "<b>Počet hlasů</b>" }, { content: "<b>Index totality</b>" }] },
					{ columns: [{ content: "Angsoc", head: true }, { content: "8" }, { content: "<i>1.4</i>" }] },
					{ columns: [{ content: "Ingsoc", head: true }, { content: "3" }, { content: "<i>1.4</i>" }] },
					{ columns: [{ content: "CCP", head: true }, { content: "2" }, { content: "<i>1.4</i>" }] },
					{ columns: [{ content: "Komunisti", head: true }, { content: "10" }, { content: "<i>1.3</i>" }] }
				]
			}]
  

## Inner
* ????????????
* Parametry
  * **type** - používá se k určení komponenty
    * "inner"
  * **columns** -
    * 1
    * 2
    * 3
    * 4
    * 5
    * 6
  * **space** -
    * number
    * string
  * **content** -
    * IElement
    * IElement[]
  * **heading** -
    * IHeading
    * string

## Cards
* ????????????
* Parametry
  * **type** - používá se k určení komponenty
    * "card"
    * "cards"
  * **content** -
    * ICardsUnit
    * ICardsUnit[]
  * **design** -
    * string
  * **heading** -
    * IHeading
    * string
* Použití

      content: [
				{
					type: "cards", content: [{
						label: "Tabulka", inner: {
							type: "inner", content: [{ type: "heading", content: "Ohlas politických stran" }, {
								type: "table",
								rows: [
									{ head: true, columns: [{ head: true, content: "<b>Strana</b>" }, { content: "<b>Počet hlasů</b>" }, { content: "<b>Index totality</b>" }] },
									{ columns: [{ content: "Angsoc", head: true }, { content: "8" }, { content: "<i>1.4</i>" }] },
									{ columns: [{ content: "Ingsoc", head: true }, { content: "3" }, { content: "<i>1.4</i>" }] },
									{ columns: [{ content: "CCP", head: true }, { content: "2" }, { content: "<i>1.4</i>" }] },
									{ columns: [{ content: "Komunisti", head: true }, { content: "10" }, { content: "<i>1.3</i>" }] }
								]
							}]
						}
					}, {
						label: "Graf", inner: {
							type: "inner", content: [{ type: "heading", content: "Ohlas politických stran" }, {
								span: 3,
								type: "media",
								source: {url: "https://cdn.pixabay.com/photo/2016/10/04/13/05/graphic-1714230_960_720.png"}
							}]
						}
					}]
				}
			]

## Media
* Funguje pro zobrazení videí, obrázků audia
* Parametry
  * **type** - používá se k určení komponenty
    * "media"
    * "image"
  * **filetype** - určuje typ zobrazeného média
    * "audio"
    * "video"
    * "image"
    * "playlist"
  * **exactMediaType** -
    * string
  * **source** - zdroj média
    * IMediaSource
    * IMediaSource[]
  * **autoplay** - automatické spuštění přehrávání při načtení
    * boolean - (true/false)
  * **replay** - Znovupřehrání videa
    * boolean - (true/false)
  * **timeline** - zobrazení časový osy
    * boolean - (true/false)
  * **script** -
    * IScript
    * {path: string}
    * {url: string}
  * **heading** - nadpis
    * IHeading
    * string
* Použití

      content: [
				{ span: 2, type: "media", source: { youtube: "rmWDIzEocpc" }, heading: "IP Freely (screw youtube)" },
				{
					span: 6,
					heading: "V jakém roce byla použita tato hudební ukázka jako hymna OH?",
					type: "imageselect",
					radio: true,
					output: { value: "test123" },
					content: [
						{ label: "1984", image: { url: "https://drwyjmricaxm7.cloudfront.net/repository/Seoul-Day-Tours-and-Activities--South-Korea--On-The-Go-Tours-435851504695803_crop_800_600.jpg" } },
						{ label: "2000", image: { url: "https://media2.s-nbcnews.com/j/newscms/2020_24/3387536/200611-seattle-autonomous-zone-al-1224_fa7ea9526005037ed63b4f95fa18d170.fit-760w.jpg" } },
						{ label: "2022", default: true, image: { url: "https://i1.wp.com/www.capitolhillseattle.com/wp-content/uploads/2020/06/CHSBLMJune92020-17.jpg" } }]
			}]

## Container
* Funguje na řazení prvků, v boxu nebo více boxech
* Parametry
  * **type** - používá se k určení komponenty
    * "container"
  * **boxCount** - počet boxů
    * 1
    * 2
  * **boxLabels** - Jmenovky boxů
    * string
    * IEmbeddedText
    * string[]
    * IEmbeddedText[]
  * **content** - obsah boxů
    * IContainerUnit
    * IContainerUnit[]
  * **recordOrder** - zapsání pořadí
    * boolean - (true/false) 
  * **showOrder** - zobrazení pořadí
    * boolean - (true/false)
  * **heading** - nadpis
    * IHeading
    * string
* Použití

      content: [{
					type: "container",
					content: [
						{
							label: "1984"
						},
						{
							label: "2008"
						},
						{
							label: "2004"
						},
						{
							label: "2014"
						},
						{
							label: "<b>1776</b>",
							backgroundColor: "silver"
						}
					]
				}]

## ~~Note~~

## ~~Include~~

## ~~Dialog~~

## ~~Catalog~~
