#!/bin/sh

cloudera_server_url="http://35.163.17.217:7180"
cloudera_api_version="3"
cluster_name="jakubaugustin"
service_name="hive"
url_suffix=""


case $1 in 
	start|stop)
		echo `date`" Performing "${service_name} " "$1" command."
		url_suffix="/commands/"$1
		http_op="POST"
	;;
	status)
		echo `date`"Performing "${service_name} " "$1" command."
		http_op="GET"
	;;
	*)
		echo "Unknown operation: "$1
		echo "usage: ./3_api_hive_state.sh start|stop|status"
		exit
	;;
esac

#Ask for username and password
read -p "Username: " USER
echo -n Password: 
read -s PASS
echo ""


assembled_url=${cloudera_server_url}"/api/v"${cloudera_api_version}"/clusters/"${cluster_name}"/services/"${service_name}${url_suffix}

echo ${assembled_url}

curl -X ${http_op} -u ${USER}:${PASS} ${assembled_url} 2> curl_out

case $1 in 
	start|stop)
	# TODO: use jq to parse JSON output and evaluate results
		echo curl_out
	;;
	status)
	# TODO: use jq to parse JSON output and evaluate results
		echo curl_out
	;;
	*)
		echo "Hic sunt leones"
		exit
	;;
esac