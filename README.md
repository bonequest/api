# BoneQuest API

* Start here: https://www.bonequest.com/api
* Please read this: https://www.bonequest.com/bots.html
* API returns JSON with a Content-Type header set to `application/json`

# Meta Payload

API responses are wrapped with meta data that may or may not be useful:

* contact = preferred email address
* high = highest episode # published so far
* queue = date when we run out of episodes queued for publication
* repo = URL to this repo
* url = base URL to website, use this to construct a fully-qualified URL for loading images and thumbnails
* version = API version

# Episode Payload

* day = day of month published
* dialog = array of arrays containing episode dialog, element 0 is typically player's name and element 1 is the dialog
* episode = episode #
* height = image height
* hd = optional, contains details about an associated BoneQuest HD image
    * author = original author, typically a Tumblr username
    * height = image height
    * id = episode #
    * image = URL to full-size image
    * link_status = empty string if URL is valid
    * mirror_url = partial URL to image if link_status is bad
    * thumb_url = partial URL to thumbnail image
    * url = fully-qualified URL to HD page
    * width = image width
* hifi = optional, contains details about an associated BoneQuest HiFi episode
    * audio_url = URL to mp3 file
    * author = who made the HiFi episode
    * create_date = date of creation in seconds since UNIX epoch
    * description = Details about the episode in plain text
    * duration = HH:MM:SS
    * hifi_id = unique HiFi ID#
    * page_url = URL to bonequesthifi.com page
* image = partial URL to episode image e.g. `/420.gif`
* month = month published, number between 1-12 
* navigation = back and next keys contain fully-formed episode for surrounding episodes
* players = array of player names
* tags = array of tags applied
* thumb = partial URL to thumbnail of episode image
* width = image width
* year = year published

## Optional Fields

Empty fields may not be present rather than returning empty strings or empty lists.

# Fetch an episode: /api/v2/episode/[EPISODE #]

Example: https://www.bonequest.com/api/v2/episode/420

# Fetch episodes: /api/v2/episodes/[LIST OF EPISODE #S, SEPARATED BY COMMA]

Example: https://www.bonequest.com/api/v2/episodes/666,667

# Fetch a random episode: /api/v2/episodes/random/[COUNT]

Example: https://www.bonequest.com/api/v2/episodes/random/1

# Fetch a random quote: /api/v2/quote/random

Example: https://www.bonequest.com/api/v2/quote/random

Similar to the episode endpoint but includes a separate `quote` key.

# Search: /api/v2/search/?q=[QUERY]

Example: https://www.bonequest.com/api/v2/search/?q=%22what+about+nuts%22

Supports these features:

* Boolean: +PERL -PISS
* Tags: #PAM-GRIER
* Dates: 8/17
* Episode #: 666
* Verbatim: "MURMPH BURMPH"

Returns an additional `search` key with this info:

* query
* runtime = time to perform query
* sums = counts of classification of results
* version = search engine version number

# Examples

## Episode Payload

```
{
    "episodes": [
        {
            "day": 20,
            "dialog": [
                [
                    "deuce",
                    "I WANT A SEX CHANGE"
                ],
                [
                    "pants",
                    "WHICH DIRECTION"
                ],
                [
                    "deuce",
                    "SURPRISE ME"
                ]
            ],
            "episode": 6969,
            "height": 574,
            "hifi": {
                "audio_url": "http://bonequesthifi.com/6969.mp3",
                "author": "BoneQuest Hi-Fi",
                "create_date": 1550592000,
                "description": "an audio production of BoneQuest #6969, featuring: @hydra2134, bonus suspended @IHaveShitMyself.\nit's time.\n~BoneQuest Hi-Fi",
                "duration": "0:30",
                "hifi_id": 501,
                "page_url": "https://bonequesthifi.com/6969"
            },
            "image": "/6969.gif",
            "month": 4,
            "navigation": {
                "back": [
                    {
                        "day": 12,
                        "dialog": [],
                        "episode": 6968,
                        "height": 383,
                        "hifi": {
                            "audio_url": "http://bonequesthifi.com/6968.mp3",
                            "author": "BoneQuest Hi-Fi",
                            "create_date": 1550160000,
                            "description": "an audio production of BoneQuest #6968, featuring: management.\nwe have jerked 500 times / and we will jerk 500 more\n~BoneQuest Hi-Fi",
                            "duration": "1:14",
                            "hifi_id": 500,
                            "page_url": "https://bonequesthifi.com/6968"
                        },
                        "image": "/6968.gif",
                        "month": 4,
                        "players": [
                            "pants",
                            "spigot"
                        ],
                        "tags": [
                            "bonequest-hi-fi",
                            "picture"
                        ],
                        "thumb": "/thumb/6968.gif",
                        "title": "thank you for pretending to give a shit",
                        "width": 575,
                        "year": 2018
                    }
                ],
                "next": [
                    {
                        "day": 21,
                        "dialog": [
                            [
                                "spigot",
                                "HOW TO SPOT A DEEP FAKE!!!!!"
                            ],
                            [
                                "spigot",
                                "STEP ONE: LOOK AT IT"
                            ]
                        ],
                        "episode": 6970,
                        "height": 574,
                        "image": "/6970.gif",
                        "month": 4,
                        "players": [
                            "spigot"
                        ],
                        "tags": [
                            "advice",
                            "deep-fake",
                            "deepfakes",
                            "how-to",
                            "mountain-background",
                            "sfw",
                            "spigot-solo"
                        ],
                        "thumb": "/thumb/6970.gif",
                        "title": "how to spot a deep fake",
                        "width": 575,
                        "year": 2018
                    }
                ]
            },
            "players": [
                "deuce",
                "pants"
            ],
            "tags": [
                "bonequest-hi-fi",
                "deuce-pants",
                "sex-change",
                "ts",
                "woodring-stairs-background"
            ],
            "thumb": "/thumb/6969.gif",
            "title": "sex change",
            "width": 575,
            "year": 2018
        }
    ],
    "meta": {
        "contact": "root@bonequest.com",
        "gay": true,
        "high": 8340,
        "queue": {
            "empty": {
                "day": 13,
                "month": 6,
                "year": 2022
            },
            "episodes": [],
            "size": 146
        },
        "repo": "https://github.com/bonequest",
        "url": "https://www.bonequest.com",
        "version": "bq/4.0.0"
    }
}
```

## Search Payload

```
{
    "episodes": [
        {
            "day": 17,
            "dialog": [
                [
                    "spigot",
                    "WHAT ABOUT NUTS"
                ],
                [
                    "spigot",
                    "WHAT ABOUT BALLS"
                ],
                [
                    "atandt",
                    "WHAT ABOUT THEM"
                ],
                [
                    "spigot",
                    "WHAT ABOUT FAT QUEER DICKS"
                ],
                [
                    "uncredited inebriated crustacean",
                    "KEEP IT DOWN"
                ]
            ],
            "episode": 2787,
            "hd": [
                {
                    "author": "eyetooth",
                    "height": 200,
                    "id": 2787,
                    "image": "http://31.media.tumblr.com/389cf0c4c9d36943f0a9aa7007e70bbf/tumblr_mlkg3kfWHP1snfhwio1_1280.png",
                    "link_status": "",
                    "mirror_url": "/hd/1.2787.jpg",
                    "thumb_url": "/hd/t/1.2787.jpg",
                    "url": "http://jerkcityhd.tumblr.com/post/48734349486/up-late",
                    "width": 144
                },
                {
                    "author": "dratomicrobotesla",
                    "height": 108,
                    "id": 2787,
                    "image": "http://41.media.tumblr.com/448b9caf05f2c92562617f00874aa494/tumblr_n8sgwzuxnq1qlfei2o1_500.jpg",
                    "link_status": "",
                    "mirror_url": "/hd/2.2787.jpg",
                    "thumb_url": "/hd/t/2.2787.jpg",
                    "url": "http://dratomicrobotesla.tumblr.com/post/91989589179",
                    "width": 144
                }
            ],
            "height": 588,
            "image": "/2787.gif",
            "month": 6,
            "players": [
                "atandt",
                "spigot"
            ],
            "tags": [
                "balls",
                "bonequest-hd",
                "dicks",
                "fighting-irish-pose",
                "inebriated-crustacean",
                "nuts",
                "queer",
                "woodring-room-background"
            ],
            "thumb": "/thumb/2787.gif",
            "title": "up late",
            "width": 588,
            "year": 2006
        }
    ],
    "meta": {
        "contact": "root@bonequest.com",
        "gay": true,
        "high": 8340,
        "repo": "https://github.com/bonequest",
        "url": "https://www.bonequest.com",
        "version": "bq/4.0.0"
    },
    "search": {
        "query": "\"what about nuts\"",
        "runtime": 0.0002644062042236328,
        "sums": {
            "dates": 0,
            "episodes": 0,
            "tags": 0,
            "titles": 0,
            "words": 1
        },
        "version": "4"
    }
}
```
