This REACT JS based web app uses the SPRING-BOOT-REST1 Api server to fetch the user table data.

STEP1 : download the file
STEP2: execute the command "npm i" to generate all node_modules
STEP3: npm start


DOCKERIZING INSTRUCTIONS
-------------------------

docker build -f Dockerfile -t react-example1 .

docker tag react-example1 naga1972/react-example1

docker push naga1972/react-example1
