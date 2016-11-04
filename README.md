Discovery containers:

sudo docker ps --format="{{.ID}} {{.Names}}" | awk 'BEGIN {count=0; id[0]=0; name[0]=0;} { id[count]=$1; name[count]=$2; count=count+1; } END { printf("{\n\t\"data\":[\n"); for(i=0;i<count;++i){ printf("\t\t{\n\t\t\t\"{#DOCKERID}\":\"%s\",\n", id[i]); printf("\t\t\t\"{#DOCKERNAME}\":\"%s\"\n\t\t}", name[i]); if(i+1<count){ printf(",\n"); } } printf("\n\t]\n}\n"); }'  | jq -r '.'
