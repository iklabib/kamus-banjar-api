<div align="center">
    <p>
        <a href="https://github.com/404NotFoundIndonesia/" target="_blank">
            <img src="https://avatars.githubusercontent.com/u/87377917?s=200&v=4" width="200" alt="404NFID Logo">
        </a>
    </p>

 [![GitHub Stars](https://img.shields.io/github/stars/iqbaleff214/kamus-banjar-api.svg)](https://github.com/iqbaleff214/kamus-banjar-api/stargazers)
 [![GitHub license](https://img.shields.io/github/license/iqbaleff214/kamus-banjar-api)](https://github.com/iqbaleff214/kamus-banjar-api/blob/main/LICENSE)
 
</div>

# Kamus Banjar API

The goal of this project is to create an API for a Banjar-Indonesian dictionary, providing users with the ability to translate words from Banjar to Indonesian.
Theoretical explanations about the Banjar language can be found on the [wiki](https://github.com/iqbaleff214/kamus-banjar-api/wiki/Tentang-Bahasa-Banjar) page.

*Read this in other languages: [Bahasa Indonesia](README.md).*

## Prerequisite

This project is built using [**Go version 1.22.2**](https://go.dev/dl/), and it is expected to be developed using this specific version of Golang to ensure the desired outcome.

## How to Run

- Install project dependencies using the command `go mod download`.
- Run the service using the command `go run .` or `go run main.go`.

## How to Test

Run the following command to perform tests:
```shell
go test -v -cover ./...
```

With this command, you can also see the test coverage level of the existing unit tests. If you make changes to the code, be sure to run the tests first to ensure all functionality still works correctly.

## How to Build

Execute the following command to build the binary:
```shell
go build -ldflags "-s -w" -o ./bin/app .
```

Then you can run the service using the command `./bin/app`.

## Usage

### [GET] /api/v1/alphabets
Returning a list of alphabet information.

#### Success response
The response will be returned an JSON. For example:
```json
{
  "code": 200,
  "data": [
    {
      "letter": "a",
      "total": 3
    }
  ],
  "message": "All alphabets successfully retrieved.",
  "status": "success"
}
```

#### Error response
The response will be returned as JSON in case of an error. For example:
```json
{
    "code": 500,
    "message": "Internal Server Error",
    "status": "error"
}
```

### [GET] /api/v1/alphabets/{letter}
Returning a list of Banjar words according to the given letter.

#### Parameters
| Name | Required | Type | Description |
| ----:|:--------:|:----:| ----------- |
| `letter` | required | param  | Alphabetic letter |

#### Success response
The response will be returned an JSON. For example:
```json
{
  "code": 200,
  "data": {
    "letter": "a",
    "total": 3,
    "words": [
      "abadan",
      "abah",
      "abat"
    ]
  },
  "message": "All words with letter 'a' successfully retrieved.",
  "status": "success"
}
```

#### Error response
The response will be returned as JSON in case of an error. For example:
```json
{
  "code": 400,
  "message": "alphabet only has one character",
  "status": "error"
}
```

### [GET] /api/v1/entries/{word}
Returning the definition and meaning according to the given Banjar word.

#### Parameters
| Name | Required | Type | Description |
| ----:|:--------:|:----:| ----------- |
| `word` | required | param  | Banjar word. |

#### Success response
The response will be returned an JSON. For example:
```json
{
  "code": 200,
  "data": {
    "word": "abah",
    "alphabet": "a",
    "meanings": [
      {
        "definitions": [
          {
            "definition": "ayah",
            "partOfSpeech": "n"
          },
          {
            "definition": "mertua laki-laki",
            "partOfSpeech": "n"
          }
        ]
      }
    ],
    "derivatives": [
      {
        "word": "baabah",
        "syllables": "ba.a.bah",
        "definitions": [
          {
            "definition": "berayah; menyebut ayah",
            "partOfSpeech": "v",
            "examples": [
              {
                "bjn": "inya kada baabah",
                "id": "dia tidak berayah"
              }
            ]
          }
        ]
      }
    ]
  },
  "message": "Definition of word 'abah' successfully retrieved.",
  "status": "success"
}
```

#### Error response
The response will be returned as JSON in case of an error. For example:
```json
{
  "code": 404,
  "message": "the word is not found",
  "status": "error"
}
```

## Reference
- [Departemen Pendidikan Nasional, Pusat Bahasa, Balai Bahasa Banjarmasin. 2008. _Kamus Bahasa Banjar Dialek Hulu-Indonesia_. Banjarbaru.](https://repositori.kemdikbud.go.id/2855/1/kamus%20bahasa%20banjar%20dialek%20hulu.pdf)
- [Pusat Pembinaan dan Pengembangan Bahasa, Departemen Pendidikan dan Kebudayaan. 1977. _Kamus Banjar-Indonesia_. Jakarta.](https://repositori.kemdikbud.go.id/2888/1/Kamus%20Banjar%20-%20Indonesia%20%20%20%20%20-%20%20%20189h.pdf)

## License

__Kamus Banjar API__ is open-sourced software licensed under the [MIT license](https://github.com/iqbaleff214/kamus-banjar-api/blob/main/LICENSE).