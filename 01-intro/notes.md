# NOTES MODULE 1

## Install libraries

*pip install tqdm notebook==7.1.2 openai elasticsearch pandas scikit-learn requests tiktoken*

## Export keys as environment variables 

*export OPENAI_API_KEY="..."*

The variables can be checked using os.environ

## Run Jupyter Notebooks

*jupyter notebook*

## Git

*git status*
*git add 01-intro/*
*git commit -m 'comments'*
*git push*

## ElasticSearch

**Running EalsticSearch:**
docker run -it \
    --rm \
    --name elasticsearch \
    -p 9200:9200 \
    -p 9300:9300 \
    -e "discovery.type=single-node" \
    -e "xpack.security.enabled=false" \
    docker.elastic.co/elasticsearch/elasticsearch:8.4.3

**Index settings:**
{
    "settings": {
        "number_of_shards": 1,
        "number_of_replicas": 0
    },
    "mappings": {
        "properties": {
            "text": {"type": "text"},
            "section": {"type": "text"},
            "question": {"type": "text"},
            "course": {"type": "keyword"} 
        }
    }
}

**Query:**
{
    "size": 5,
    "query": {
        "bool": {
            "must": {
                "multi_match": {
                    "query": query,
                    "fields": ["question^3", "text", "section"],
                    "type": "best_fields"
                }
            },
            "filter": {
                "term": {
                    "course": "data-engineering-zoomcamp"
                }
            }
        }
    }
}