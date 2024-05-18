# DevOps CapStone Project Applications Deployment

### Project [GitHub Repo URL](https://github.com/psaineeraj0301/FinalProject)
### Project [Doc](https://docs.google.com/document/d/1raDCcOAkHiSI_vIy3itm25r5TcNS6mJuPx-CNOY9F7Y/edit?usp=sharing)
### Running [Project App](http://ec2-35-160-146-190.us-west-2.compute.amazonaws.com/)
<br >
Branch<br >
> - `master`<br >
> - `dev`

## AWS setup
1. **Security Group**
   > Inbound Rule<br >
   ![Inbound Rule-1](./assets/Sg_inbound.png) <br >
   ![Inbound Rule-2](./assets/Sg_inbound2.png) <br >
   > Outbound Rule<br >
   ![Outbound Rule](./assets/Sg_outbound.png) <br >

2. **EC2 Console**
   ![EC2 Console](./assets/EC2_console.png) <br >

## Jenkins
1. **Jenkins Login**
   ![Jenkins Login](./assets/jenkins_login.jpg) <br >
2. **Configuration**
   - Docker Plugin<br >
   ![Docker Plugin](./assets/jenkins_docker_plugin.png) <br >
   - GitHub Server Connection <br >
   ![Github Server Connection](./assets/jenkins_github_server.png) <br >
   - PipeLine
     ![PipeLine](./assets/jenkins_pipeline1.png) <br >
3. **Execution Steps**
   - PipeLine Stage View<br >
   ![PipeLine Stage View](./assets/jenkins_stageview.jpg) <br >

## Docker Hub
1. Docker Hub Dashboard with `prod` *private* repo and `dev` *public* repo
   ![Docker HUb Dashboard](./assets/dockerhub_dashboard.png) <br >
2. Prod Repo with images<br >![Docker Prod](./assets/dockerhub_prod_repo.png)<br >
3. Dev Repo with images<br >![Docker Prod](./assets/dockerhub_dev_repo.png)<br >

## Deployed App<br >
![Deployed React App](./assets/react_app.png)<br >
## Monitoring
### Prometheus
1. Prometheus Graph<br > ![Prometheus Graph](./assets/prometheus_graph.png) <br >
2. Prometheus Console<br > ![Prometheus Console](./assets/prometheus_console.png) <br >

### Grafana
1. Grafana Dashboard<br >
![Grafan Dashboard](./assets/grafana_dashboard.png) <br >
  - Grafana Metric<br >
  ![Grafan Metric](./assets/grafana_metric.png) <br >


