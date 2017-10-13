---
title: "Requests"
teaching: 15
exercises: 20
questions:
- "What is a HTTP request?"
- "How can I use `requests` to get data?"
- "What does a request return?"
objectives:
- "Get data from an API using the `requests` library."
- "Know the difference between and API endpoint and regular URL and the types of data they return."
keypoints:
- "HTTP requests are a way to transfer data over the internet."
- "HTTP GET requests take a URL as a parameter and return data to you programmatically."
- "An API is a web address designed to provide data programmatically."
- "The `requests` library makes HTTP requests easier."
- "The `simplejson` makes working with JSON data easier."
---

## Use `requests` to grab data from the web

* The Python `requests` library will do a lot of the work for you.

~~~
import requests
help(requests)
~~~
{: .python}


~~~
Help on package requests:

NAME
    requests

DESCRIPTION
    Requests HTTP Library
    ~~~~~~~~~~~~~~~~~~~~~
    
    Requests is an HTTP library, written in Python, for human beings. Basic GET
    usage:
    
import requests
r = requests.get('https://www.python.org')
r.status_code
       200
'Python is a programming language' in r.content
       True
    
or POST:
    
payload = dict(key1='value1', key2='value2')
r = requests.post('http://httpbin.org/post', data=payload)
print(r.text)
       {
         ...
         "form": {
           "key2": "value2",
           "key1": "value1"
         },
         ...
       }
    
    The other HTTP methods are supported - see `requests.api`. Full documentation
    is at <http://python-requests.org>.
    
    :copyright: (c) 2017 by Kenneth Reitz.
    :license: Apache 2.0, see LICENSE for more details.

PACKAGE CONTENTS
    __version__
    _internal_utils
    adapters
    api
    auth
    certs
    compat
    cookies
    exceptions
    help
    hooks
    models
    packages
    sessions
    status_codes
    structures
    utils

FUNCTIONS
    check_compatibility(urllib3_version, chardet_version)

DATA
    __author_email__ = 'me@kennethreitz.org'
    __build__ = 137220
    __cake__ = '✨ 🍰 ✨'
    __copyright__ = 'Copyright 2017 Kenneth Reitz'
    __description__ = 'Python HTTP for Humans.'
    __license__ = 'Apache 2.0'
    __title__ = 'requests'
    __url__ = 'http://python-requests.org'
    codes = <lookup 'status_codes'>

VERSION
    2.18.4

AUTHOR
    Kenneth Reitz

~~~
{: .output}


## Make a GET Request: Just Like A Browser*

*   The most common type of request is a GET request, and the only parameter it requires is a URL. Like a web browser with only text.
*   Save the response by assigning the request to a variable:

~~~
response = requests.get('https://open.library.ubc.ca') # calling the output of a request "response" is a convention
print(response)
~~~
{: .python}

~~~
# 200 means it worked!
<Response [200]>
~~~
{: .output}


*  `requests` prints the "response code" sent by the server at that address. 200 is good. 404 is bad. There are [many others](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)


## Get at the Data
*   The `request` object (that we saved as `oc_home`) holds much more than just the response code, and has specific methods available to reveal its secrets.
*   `request.url` will show the url (you can double check it's the right one)
*   `request.text` will read the "payload" from the server.
*   `request.json()` will decode an endpoint that returns JSON data (more on that soon)

~~~
print(response.url)
print(response.text[:1000]) # this can be really long, so we'll ask for only the first 1000 characters of it.
~~~
{: .python}

~~~
<Response [200]>
https://open.library.ubc.ca/
    
<!DOCTYPE html>
  
<!--[if IEMobile 7]>
<html class="iem7 oldie" lang="en">
<![endif]-->
<!--[if (IE 7)&!(IEMobile)]>
<html class="ie7 oldie" lang="en">
<![endif]-->
<!--[if (IE 8)&!(IEMobile)]>
<html class="ie8 oldie" lang="en">
<![endif]-->
<!--[if (IE 9)&!(IEMobile)]>
<html class="ie9" lang="en">
<![endif]-->
<!--[[if (gt IE 9)|(gt IEMobile 7)]>
<!-->
<html lang="en">
<!--<![endif]-->

<!--
 * UBC CLF (Common Look and Feel) v7.0.2
 * Copyright 2012 The University of British Columbia
 * UBC Communications and Marketing
 * http://brand.ubc.ca/clf
 */
-->

<head>
                <!-- HEAD -->
    
  <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <meta name="description" content="Learning, knowledge, research, insight: welcome to the world of UBC Library, the second-largest academic research library in Canada.">
  <meta name="author" content="">
    
  <!-- CLF Stylesheets -->
  <l

~~~
{: .output}

*   Do you recognize this? Is this useful?

~~~
print(response.url)
print(response.json())
~~~
{: .python}

~~~
<Response [200]>
https://open.library.ubc.ca/
<bound method Response.json of <Response [200]>>
~~~
{: .output}

*   Where is the data?


## API Endpoints Return Data in Useful Formats

*   Any web address will return its data to a GET request, but sifting through it to get to any meaningful information is tedious.
*   API (Anyone know what it stands for?) endpoints return raw data without all of the HTML markup.
    *   Commonly as JSON or XML. These are easier to work with programmatically.
*   UBC Library's Open Collections (OC) has a [public API](https://open.library.ubc.ca/docs) at `oc-index.library.ubc.ca`


~~~
# get a list of the available collections
oc_collections = requests.get('https://oc-index.library.ubc.ca/collections')
print(oc_collections.url)
print(oc_collections.json())
~~~
{: .python}

~~~
print(oc_collections.url)
https://oc-index.library.ubc.ca/collections
{'http_code': 200, 'endpoint': 'GET: /collections', 'api_code': 3000, 'api_text': 'List all Collections | API Version: 1', 'user_ip': '137.82.99.125', 'data': {'0': 'aaah', '3': 'abacusopen', '5': 'advance', '6': 'agassiz', '7': 'alumchron', '8': 'anderson', '9': 'archivesav', '12': 'ardeau', '15': 'arkley', '17': 'arlaadvo', '18': 'armstrongad', '20': 'arphotos', '24': 'artefacts', '25': 'asian', '27': 'bcbooks', '42': 'bcfed', '45': 'bch', '46': 'bcln', '47': 'bclumber', '48': 'bcnews', '49': 'bcret', '50': 'bcsessional', '58': 'bct', '60': 'bctu', '61': 'beaverdell', '62': 'bensun', '63': 'berkpost', '65': 'biblos', '66': 'bookplate', '70': 'brooklynnews', '72': 'bullock', '74': 'calendars', '75': 'canford', '76': 'capilano', '77': 'cascade', '80': 'cassiarnews', '83': 'cflacla', '86': 'cg', '87': 'chasetrib', '89': 'chilliwackfp', '91': 'chungex', '92': 'chungobject', '94': 'chungosgr', '98': 'chungphotos', '104': 'chungpub', '108': 'chungtext', '125': 'chungvoyager', '127': 'citizennw', '129': 'citraudio', '131': 'coalmont', '132': 'coasmine', '133': 'columbiarev', '134': 'courtenayrev', '138': 'cranbrookpro', '140': 'cranherald', '144': 'creelman', '145': 'croftongaz', '146': 'cumberlandis', '149': 'cwn', '152': 'darwin', '154': 'davidconde', '155': 'davidsonia', '156': 'daytele', '158': 'dbc', '161': 'dcanadi', '166': 'delgamuukw', '169': 'deltnews', '171': 'delttime', '173': 'despatch', '174': 'discorder', '181': 'disledfer', '185': 'djcox', '187': 'dorothyburn', '188': 'dtv', '190': 'eastkootmine', '192': 'echo', '193': 'ecrosby', '194': 'enterprise', '195': 'epnoh', '197': 'etheljohns', '198': 'eveningt', '199': 'evenkoot', '200': 'evewoross', '204': 'expressnv', '207': 'feeders', '209': 'fernieled', '211': 'fgherald', '213': 'fisheries', '217': 'fisherman', '220': 'florence', '222': 'focus', '224': 'framed', '227': 'fraseradvanc', '230': 'gcdb', '231': 'gfminer', '232': 'glennews', '233': 'goldenera', '236': 'goldentimes', '239': 'greemine', '241': 'gvchinook', '244': 'gvrdmaps', '246': 'hawthorn', '250': 'holland', '253': 'hqueek', '255': 'htbva', '256': 'htimes', '258': 'hundred', '266': 'iel', '268': 'indworld', '270': 'jphotos', '272': 'kerechro', '274': 'kinesis', '275': 'koolib', '276': 'kootstar', '279': 'kwawa', '280': 'laborstar', '282': 'ladysmithl', '283': 'ladysmithr', '284': 'ladysmithsi', '285': 'ladysmithst', '286': 'langmann', '289': 'lardeaum', '291': 'leadera', '292': 'ledge', '295': 'ledgefern', '296': 'ledgenel', '297': 'libsenrep', '302': 'lilladva', '305': 'locla', '306': 'macmillan', '308': 'manuscripts', '309': 'marytrib', '310': 'mathison', '311': 'mccormick', '313': 'mherald', '317': 'michelr', '320': 'misscity', '321': 'mmention', '323': 'mminer', '324': 'morninglnw', '326': 'mpadvocate', '328': 'nanacour', '330': 'nanamail', '333': 'ndaymine', '337': 'newestimes', '339': 'nicoheral', '340': 'norcoa', '341': 'nursing', '342': 'nwdn', '345': 'nwminer', '346': 'ohs', '349': 'omineca', '351': 'ominecaminer', '352': 'omr', '353': 'paccannw', '355': 'paystreak', '358': 'peloyalist', '360': 'penpress', '362': 'pmgazette', '365': 'presrep', '367': 'princero', '370': 'prism', '371': 'prj', '373': 'proslill', '374': 'prossross', '376': 'pwv', '379': 'qcislander', '381': 'qcminer', '382': 'rainbow', '393': 'redflag', '394': 'rosetti', '395': 'royalfisk', '397': 'saga', '398': 'satworld', '399': 'senmin', '401': 'sfjcbce', '402': 'silsil', '404': 'slocanp', '406': 'slodrill', '409': 'slorec', '410': 'smreview', '413': 'specialp', '415': 'squeezes', '418': 'surreytimes', '419': 'tairikunipp', '428': 'tgdp', '430': 'the432', '431': 'thenugget', '434': 'thestar', '435': 'thesun', '436': 'thewave', '437': 'tokugawa', '439': 'touchpoints', '440': 'ubcavfrc', '442': 'ubchist', '443': 'ubclibnews', '446': 'ubclsmm', '448': 'ubcmedicine', '449': 'ubcreports', '453': 'ubcstuhan', '454': 'ubctp', '457': 'ubcyearb', '459': 'ubysseynews', '466': 'upubmisc', '467': 'vanad', '468': 'vanbuildrec', '470': 'vma', '472': 'vslp', '473': 'vyg', '475': 'wclarion', '478': 'westho', '480': 'westland', '482': 'wwiphoto', '485': 'wwposters', '487': 'xabpost', '488': 'xalberniadv', '489': 'xanaconda', '491': 'xatlin', '493': 'xbcrecord', '494': 'xbellacoo', '496': 'xboundarycr', '499': 'xcariboosen', '502': 'xcoastnews', '507': 'xcrestonrev', '509': 'xcumberland', '513': 'xdailyledg', '517': 'xdbr', '519': 'xenderby', '523': 'xgrandforks', '527': 'xhedley', '530': 'xhotsprings', '533': 'xindependen', '535': 'xkelownarec', '538': 'xkootmail', '540': 'xledgreen', '544': 'xmassett', '545': 'xminer', '549': 'xminingrev', '553': 'xmoyie', '554': 'xnakledge', '557': 'xnelsonecon', '560': 'xnicola', '563': 'xpentimes', '566': 'xphoenix', '571': 'xprospector', '572': 'xrevherald', '575': 'xtribune', '578': 'xwestcall', '580': 'yipsang', '582': 'ymirherald', '583': 'ymirminer', '584': 'ymirmirror', '585': 24, '607': 310, '611': 494, '613': 641, '615': 801, '616': 831, '636': 2689, '638': 11568, '639': 11569, '640': 11570, '641': 11571, '642': 12708, '646': 13139, '647': 18861, '654': 23302, '655': 23303, '656': 23304, '657': 23553, '658': 25332, '659': 26856, '660': 27306, '665': 29912, '666': 29962, '667': 31775, '668': 31776, '669': 32457, '670': 32618, '671': 33381, '672': 33426, '674': 33755, '675': 33850, '676': 34295, '677': 40947, '678': 42020, '679': 42446, '680': 42591, '686': 43377, '687': 43962, '689': 44311, '690': 46624, '691': 46718, '692': 46721, '693': 48630, '702': 50555, '703': 51833, '705': 51869, '706': 52383, '725': 52387, '732': 52657, '733': 52660, '736': 52966, '745': 53032, '749': 53169, '752': 53926, '753': 55474, '754': 58233, '755': 59278, '757': 59367, '762': 59368, '766': 59369, '767': 59370, '768': 59371, '769': 59374, '770': 59404, '771': 59405, '772': 59406, '773': 59585, '774': 59757, '775': 60499, '776': 62152}}
~~~
{: .output}

*   Now we have raw data without all of the HTML markup, if only it were easier to read...


## Use `json` to Make JSON More Legible

*   `json` is a library for making it easier to work with JSON data in Python.
*   It can be used to "pretty print" JSON data to make it easier for humans to read
    *   Use the 'indent' argument to add spaces to structure the data.


~~~
import json

human_readable = json.dumps(oc_collections.json(), indent=2*" ")
print(human_readable)
~~~
{: .python}

~~~

https://oc-index.library.ubc.ca/collections
{
    "http_code": 200,
    "endpoint": "GET: /collections",
    "api_code": 3000,
    "api_text": "List all Collections | API Version: 1",
    "user_ip": "137.82.99.125",
    "data": {
        "0": "aaah",
        "3": "abacusopen",
        "5": "advance",
        "6": "agassiz",
        "7": "alumchron",
        "8": "anderson",
        "9": "archivesav",
        "12": "ardeau",
        "15": "arkley",
        "17": "arlaadvo",
        "18": "armstrongad",
        "20": "arphotos",
        "24": "artefacts",
        "25": "asian",
        "27": "bcbooks",
        "42": "bcfed",
        "45": "bch",
        "46": "bcln",
        "47": "bclumber",
        "48": "bcnews",
        "49": "bcret",
        "50": "bcsessional",
        "58": "bct",
        "60": "bctu",
        "61": "beaverdell",
        "62": "bensun",
        "63": "berkpost",
        "65": "biblos",
        "66": "bookplate",
        "70": "brooklynnews",
        "72": "bullock",
        "74": "calendars",
        "75": "canford",
        "76": "capilano",
        "77": "cascade",
        "80": "cassiarnews",
        "83": "cflacla",
        "86": "cg",
        "87": "chasetrib",
        "89": "chilliwackfp",
        "91": "chungex",
        "92": "chungobject",
        "94": "chungosgr",
        "98": "chungphotos",
        "104": "chungpub",
        "108": "chungtext",
        "125": "chungvoyager",
        "127": "citizennw",
        "129": "citraudio",
        "131": "coalmont",
        "132": "coasmine",
        "133": "columbiarev",
        "134": "courtenayrev",
        "138": "cranbrookpro",
        "140": "cranherald",
        "144": "creelman",
        "145": "croftongaz",
        "146": "cumberlandis",
        "149": "cwn",
        "152": "darwin",
        "154": "davidconde",
        "155": "davidsonia",
        "156": "daytele",
        "158": "dbc",
        "161": "dcanadi",
        "166": "delgamuukw",
        "169": "deltnews",
        "171": "delttime",
        "173": "despatch",
        "174": "discorder",
        "181": "disledfer",
        "185": "djcox",
        "187": "dorothyburn",
        "188": "dtv",
        "190": "eastkootmine",
        "192": "echo",
        "193": "ecrosby",
        "194": "enterprise",
        "195": "epnoh",
        "197": "etheljohns",
        "198": "eveningt",
        "199": "evenkoot",
        "200": "evewoross",
        "204": "expressnv",
        "207": "feeders",
        "209": "fernieled",
        "211": "fgherald",
        "213": "fisheries",
        "217": "fisherman",
        "220": "florence",
        "222": "focus",
        "224": "framed",
        "227": "fraseradvanc",
        "230": "gcdb",
        "231": "gfminer",
        "232": "glennews",
        "233": "goldenera",
        "236": "goldentimes",
        "239": "greemine",
        "241": "gvchinook",
        "244": "gvrdmaps",
        "246": "hawthorn",
        "250": "holland",
        "253": "hqueek",
        "255": "htbva",
        "256": "htimes",
        "258": "hundred",
        "266": "iel",
        "268": "indworld",
        "270": "jphotos",
        "272": "kerechro",
        "274": "kinesis",
        "275": "koolib",
        "276": "kootstar",
        "279": "kwawa",
        "280": "laborstar",
        "282": "ladysmithl",
        "283": "ladysmithr",
        "284": "ladysmithsi",
        "285": "ladysmithst",
        "286": "langmann",
        "289": "lardeaum",
        "291": "leadera",
        "292": "ledge",
        "295": "ledgefern",
        "296": "ledgenel",
        "297": "libsenrep",
        "302": "lilladva",
        "305": "locla",
        "306": "macmillan",
        "308": "manuscripts",
        "309": "marytrib",
        "310": "mathison",
        "311": "mccormick",
        "313": "mherald",
        "317": "michelr",
        "320": "misscity",
        "321": "mmention",
        "323": "mminer",
        "324": "morninglnw",
        "326": "mpadvocate",
        "328": "nanacour",
        "330": "nanamail",
        "333": "ndaymine",
        "337": "newestimes",
        "339": "nicoheral",
        "340": "norcoa",
        "341": "nursing",
        "342": "nwdn",
        "345": "nwminer",
        "346": "ohs",
        "349": "omineca",
        "351": "ominecaminer",
        "352": "omr",
        "353": "paccannw",
        "355": "paystreak",
        "358": "peloyalist",
        "360": "penpress",
        "362": "pmgazette",
        "365": "presrep",
        "367": "princero",
        "370": "prism",
        "371": "prj",
        "373": "proslill",
        "374": "prossross",
        "376": "pwv",
        "379": "qcislander",
        "381": "qcminer",
        "382": "rainbow",
        "393": "redflag",
        "394": "rosetti",
        "395": "royalfisk",
        "397": "saga",
        "398": "satworld",
        "399": "senmin",
        "401": "sfjcbce",
        "402": "silsil",
        "404": "slocanp",
        "406": "slodrill",
        "409": "slorec",
        "410": "smreview",
        "413": "specialp",
        "415": "squeezes",
        "418": "surreytimes",
        "419": "tairikunipp",
        "428": "tgdp",
        "430": "the432",
        "431": "thenugget",
        "434": "thestar",
        "435": "thesun",
        "436": "thewave",
        "437": "tokugawa",
        "439": "touchpoints",
        "440": "ubcavfrc",
        "442": "ubchist",
        "443": "ubclibnews",
        "446": "ubclsmm",
        "448": "ubcmedicine",
        "449": "ubcreports",
        "453": "ubcstuhan",
        "454": "ubctp",
        "457": "ubcyearb",
        "459": "ubysseynews",
        "466": "upubmisc",
        "467": "vanad",
        "468": "vanbuildrec",
        "470": "vma",
        "472": "vslp",
        "473": "vyg",
        "475": "wclarion",
        "478": "westho",
        "480": "westland",
        "482": "wwiphoto",
        "485": "wwposters",
        "487": "xabpost",
        "488": "xalberniadv",
        "489": "xanaconda",
        "491": "xatlin",
        "493": "xbcrecord",
        "494": "xbellacoo",
        "496": "xboundarycr",
        "499": "xcariboosen",
        "502": "xcoastnews",
        "507": "xcrestonrev",
        "509": "xcumberland",
        "513": "xdailyledg",
        "517": "xdbr",
        "519": "xenderby",
        "523": "xgrandforks",
        "527": "xhedley",
        "530": "xhotsprings",
        "533": "xindependen",
        "535": "xkelownarec",
        "538": "xkootmail",
        "540": "xledgreen",
        "544": "xmassett",
        "545": "xminer",
        "549": "xminingrev",
        "553": "xmoyie",
        "554": "xnakledge",
        "557": "xnelsonecon",
        "560": "xnicola",
        "563": "xpentimes",
        "566": "xphoenix",
        "571": "xprospector",
        "572": "xrevherald",
        "575": "xtribune",
        "578": "xwestcall",
        "580": "yipsang",
        "582": "ymirherald",
        "583": "ymirminer",
        "584": "ymirmirror",
        "585": 24,
        "607": 310,
        "611": 494,
        "613": 641,
        "615": 801,
        "616": 831,
        "636": 2689,
        "638": 11568,
        "639": 11569,
        "640": 11570,
        "641": 11571,
        "642": 12708,
        "646": 13139,
        "647": 18861,
        "654": 23302,
        "655": 23303,
        "656": 23304,
        "657": 23553,
        "658": 25332,
        "659": 26856,
        "660": 27306,
        "665": 29912,
        "666": 29962,
        "667": 31775,
        "668": 31776,
        "669": 32457,
        "670": 32618,
        "671": 33381,
        "672": 33426,
        "674": 33755,
        "675": 33850,
        "676": 34295,
        "677": 40947,
        "678": 42020,
        "679": 42446,
        "680": 42591,
        "686": 43377,
        "687": 43962,
        "689": 44311,
        "690": 46624,
        "691": 46718,
        "692": 46721,
        "693": 48630,
        "702": 50555,
        "703": 51833,
        "705": 51869,
        "706": 52383,
        "725": 52387,
        "732": 52657,
        "733": 52660,
        "736": 52966,
        "745": 53032,
        "749": 53169,
        "752": 53926,
        "753": 55474,
        "754": 58233,
        "755": 59278,
        "757": 59367,
        "762": 59368,
        "766": 59369,
        "767": 59370,
        "768": 59371,
        "769": 59374,
        "770": 59404,
        "771": 59405,
        "772": 59406,
        "773": 59585,
        "774": 59757,
        "775": 60499,
        "776": 62152
    }
}
~~~
{: .output}

## Get at specific data values by transforming JSON into a dictionary

*   The JSON structure may look familiar: It shares a 'key-value' structure with Python's 'dictionary' data type.
*   The `json()` method we've been using from the `request` library converts the response JSON data into a dictionary.
*   Use bracket notation to access the desired data.


~~~
import json

human_readable = json.dumps(oc_collections.json(), indent=2*" ")
print(human_readable)
~~~
{: .python}




> ## Print the collection metadata for the Open Collection's 'arkley' collection
>
> The Open Collections API documentation has a list of available endpoints and examples at [https://open.library.ubc.ca/docs#api-requests](https://open.library.ubc.ca/docs#api-requests). 
> Use a GET request to return and then "pretty print" the metadata associated with the 'arkley' collection. What is its overarching theme?
>
> > ## Solution
> >
> > `import json, requests`
> > `response = requests.get('https://oc-index.library.ubc.ca/collections/arkley')`
> > `print(json.dumps(response.json(), indent=2*" "))`
> {: .solution}
{: .challenge}


> ## Print the metadata for an item from Open Collection's 'arkley' collection
> 
> Use a GET request to return and then "pretty print" the metadata associated with a specific item from the 'arkley' collection. 
> Hint: You can request a list of the first 100 items in the collection at https://oc-web.library.ubc.ca/collections/arkley/items?limit=100
>
> > ## Solution
> >
> > `import json, requests`
> > `items = requests.get(https://oc-web.library.ubc.ca/collections/arkley/items?limit=100)`
> > `print(json.dumps(response.json(), indent=2*" "))`
> > `# copy an item id`
> > `response = requests.get('response = requests.get('https://oc-index.library.ubc.ca/collections/arkley/items/1.0010491')')`
> > `print(json.dumps(response.json(), indent=2*" "))`
> {: .solution}
{: .challenge}


> ## Print the item's title, creator, and description
> 
> Hint: Look carefully at the JSON you pretty-printed. Remember, square brackets indicates a list and curly brackets a dictionary. Lists items are accessed by index and dictionary items by key.
>
> > ## Solution
> >
> > `metadata = response.json()['data']`
> > `print(metadata['Title'][0]['value'])`
> > `print(metadata['Creator'][0]['value'])`
> > `print(metadata['Description'][0]['value'])`
> {: .solution}
{: .challenge}