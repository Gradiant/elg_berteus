# elg_berteus
elg_berteus is a tool that predicts which word fits in a masked space on a basque text using the masked language model BERTEUS.
This repository contains a dockerized API built over BERTEUS for integrate it into the ELG.

## Install

```
sh docker-build.sh
```

## Execute
```
docker run --rm -p 0.0.0.0:8866:8866 --name berteus elg_berteus:1.0
```
## Use

```
curl -X POST  http://0.0.0.0:8866/predict_json -H 'Content-Type: application/json' -d '{"type": "text", "content":" Egun [MASK] izan dezala "}'
```


# Test
In the folder `test` you have the files for testing the API according to the ELG specifications.
It uses an API that acts as a proxy with your dockerized API that checks both the requests and the responses.
For this follow the instructions:
1) Configure the .env file with the data of the image and your API
2) Launch the test: `docker-compose up`
3) Make the requests, instead of to your API's endpoint, to the test's endpoint:
   ```
   curl -X POST  http://0.0.0.0:8866/processText/service -H 'Content-Type: application/json' -d '{"type": "text", "content":" Egun [MASK] izan dezala "}'
   ```
4) If your request and the API's response is compliance with the ELG API, you will receive the response.
   1) If the request is incorrect: Probably you will don't have a response and the test tool will not show any message in logs.
   2) If the response is incorrect: You will see in the logs that the request is proxied to your API, that it answers, but the test tool does not accept that response. You must analyze the logs.


## Citations:
The original work of this tool is:
- Agerri, R., Vicente, I. S., Campos, J. A., Barrena, A., Saralegi, X., Soroa, A., & Agirre, E. (2020). Give your text representation models some love: the case for basque. arXiv preprint arXiv:2004.00033.
