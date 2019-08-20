---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-31"

keywords: kubernetes, iks, ibmcloud, ic, ks, ibmcloud ks

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# {{site.data.keyword.containerlong_notm}}-CLI
{: #kubernetes-service-cli}

Verwenden Sie diese Befehle, um **sowohl Community-Kubernetes-Cluster als auch OpenShift-Cluster** in {{site.data.keyword.containerlong}} zu erstellen und zu verwalten.
{:shortdesc}

* **Community-Kubernetes**: [Installieren Sie das CLI-Plug-in](/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps), das den Aliasnamen `ibmcloud ks` verwendet.
* **OpenShift**: [Installieren Sie das CLI-Plug-in](/docs/openshift?topic=openshift-openshift-cli), das den Aliasnamen `ibmcloud oc` verwendet.

Sie werden im Terminal benachrichtigt, wenn Aktualisierungen für die `ibmcloud`-CLI und -Plug-ins verfügbar sind. Halten Sie Ihre CLI stets aktuell, sodass Sie alle verfügbaren Befehle und Flags verwenden können.

Suchen Sie nach `ibmcloud cr`-Befehlen? Werfen Sie einen Blick in die [{{site.data.keyword.registryshort_notm}}-CLI-Referenz ](/docs/services/Registry?topic=container-registry-cli-plugin-containerregcli). Suchen Sie nach `kubectl`-Befehlen? Werfen Sie einen Blick in die [Kubernetes-Dokumentation ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubectl.docs.kubernetes.io/).
{:tip}

## {{site.data.keyword.containerlong_notm}}-Plug-in der Betaversion verwenden
{: #cs_beta}

Eine überarbeitete Version des {{site.data.keyword.containerlong_notm}}-Plug-ins ist als Betaversion verfügbar. In der überarbeiteten Version des {{site.data.keyword.containerlong_notm}}-Plug-ins werden Befehle zu Kategorien zusammengruppiert und die Befehle von einer Struktur mit Bindestrichen in eine Struktur mit Leerzeichen geändert. Außerdem ist ab Betaversion `0.3` (Standard) eine neue [globale Endpunktfunktionalität](/docs/containers?topic=containers-regions-and-zones#endpoint) verfügbar.
{: shortdesc}

Die folgenden Betaversionen des überarbeiteten {{site.data.keyword.containerlong_notm}}-Plug-ins sind verfügbar.
* Das Standardverhalten ist `0.3`. Stellen Sie sicher, dass Ihr {{site.data.keyword.containerlong_notm}}-Plug-in die neueste `0.3`-Version verwendet, indem Sie `ibmcloud plugin update kubernetes-service` ausführen.
* Zur Verwendung von `0.4` oder `1.0` setzen Sie die Umgebungsvariable `IKS_BETA_VERSION` auf die Betaversion, die Sie verwenden möchten:
    ```
    export IKS_BETA_VERSION=<betaversion>
    ```
    {: pre}
* Um die veraltete Funktionalität regionaler Endpunkte zu verwenden, müssen Sie mit dem Befehl [`init` den regionalen Endpunkt als Ziel angeben](#cs_init).
    ```
    ibmcloud ks init --host <regionaler_endpunkt>
    ```
    {: pre}

</br>

<table>
<caption>Betaversionen des überarbeiteten {{site.data.keyword.containerlong_notm}}-Plug-ins</caption>
  <thead>
    <th>Betaversion</th>
    <th>Ausgabestruktur für `ibmcloud ks help`</th>
    <th>Befehlsstruktur</th>
    <th>Standortfunktionalität</th>
  </thead>
  <tbody>
    <tr>
      <td><code>0.2</code> (veraltet)</td>
      <td>Vorherige Version: Befehle werden in der Struktur mit Bindestrichen angezeigt und alphabetisch aufgelistet.</td>
      <td>Vorherige und Betaversion: Sie können Befehle entweder in der vorherigen Struktur mit Bindestrichen (`ibmcloud ks alb-cert-get`) oder in der Betastruktur mit Leerzeichen (`ibmcloud ks alb cert get`) ausführen.</td>
      <td>Regional: [Geben Sie eine Region als Ziel an und verwenden Sie einen regionalen Endpunkt, um mit Ressourcen in dieser Region zu arbeiten](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>0.3</code> (Standard)</td>
      <td>Vorherige Version: Befehle werden in der Struktur mit Bindestrichen angezeigt und alphabetisch aufgelistet.</td>
      <td>Vorherige und Betaversion: Sie können Befehle entweder in der vorherigen Struktur mit Bindestrichen (`ibmcloud ks alb-cert-get`) oder in der Betastruktur mit Leerzeichen (`ibmcloud ks alb cert get`) ausführen.</td>
      <td>Global: [Globalen Endpunkt verwenden, um mit Ressourcen an einem beliebigen Standort zu arbeiten](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>0.4</code></td>
      <td>Betaversion: Befehle werden in der Struktur mit Leerzeichen angezeigt und in Kategorien aufgelistet.</td>
      <td>Vorherige und Betaversion: Sie können Befehle entweder in der vorherigen Struktur mit Bindestrichen (`ibmcloud ks alb-cert-get`) oder in der Betastruktur mit Leerzeichen (`ibmcloud ks alb cert get`) ausführen.</td>
      <td>Global: [Globalen Endpunkt verwenden, um mit Ressourcen an einem beliebigen Standort zu arbeiten](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
    <tr>
      <td><code>1.0</code></td>
      <td>Betaversion: Befehle werden in der Struktur mit Leerzeichen angezeigt und in Kategorien aufgelistet.</td>
      <td>Betaversion: Sie können Befehle nur in der Betastruktur mit Leerzeichen (`ibmcloud ks alb cert get`) ausführen.</td>
      <td>Global: [Globalen Endpunkt verwenden, um mit Ressourcen an einem beliebigen Standort zu arbeiten](/docs/containers?topic=containers-regions-and-zones#bluemix_regions).</td>
    </tr>
  </tbody>
</table>



<br />


## API-Befehle
{: #api_commands}

### `ibmcloud ks api`
{: #cs_cli_api}

Legt den API-Endpunkt als Ziel für {{site.data.keyword.containerlong_notm}} fest. Wenn Sie keinen Endpunkt angeben, können Sie Informationen zu dem aktuellen Endpunkt anzeigen, der als Ziel angegeben wurde.
{: shortdesc}

Regionsspezifische Endpunkte werden nicht mehr verwendet. Verwenden Sie stattdessen den [globalen Endpunkt](/docs/containers?topic=containers-regions-and-zones#endpoint). Wenn Sie regionale Endpunkte verwenden müssen, [setzen Sie die Umgebungsvariable `IKS_BETA_VERSION` im {{site.data.keyword.containerlong_notm}}-Plug-in auf `0.2`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta).
{: deprecated}

Wenn Sie nur Ressourcen aus einer Region auflisten und mit ihnen arbeiten müssen, können Sie den Befehl `ibmcloud ks api` verwenden, um einen regionalen Endpunkt anstelle des globalen Endpunkts zu verwenden.
* Dallas (Vereinigte Staaten (Süden), us-south): `https://us-south.containers.cloud.ibm.com`
* Frankfurt (Mitteleuropa, eu-de): `https://eu-de.containers.cloud.ibm.com`
* London (Vereinigtes Königreich (Süden), eu-gb): `https://eu-gb.containers.cloud.ibm.com`
* Sydney (Asien-Pazifik (Süden), au-syd): `https://au-syd.containers.cloud.ibm.com`
* Tokio (Asien-Pazifik (Norden), jp-tok): `https://jp-tok.containers.cloud.ibm.com`
* Washington, D.C. (Vereinigte Staaten (Osten), us-east): `https://us-east.containers.cloud.ibm.com`

Um die globale Funktionalität zu verwenden, können Sie den Befehl `ibmcloud ks api` erneut verwenden, um den globalen Endpunkt als Ziel festzulegen: `https://containers.cloud.ibm.com`

```
ibmcloud ks api --endpoint ENDPUNKT [--insecure] [--skip-ssl-validation] [--api-version WERT] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen**:
<dl>
<dt><code>--endpoint <em>ENDPUNKT</em></code></dt>
  <dd>Der {{site.data.keyword.containerlong_notm}}-API-Endpunkt. <strong>Hinweis</strong>: Dieser Endpunkt unterscheidet sich von {{site.data.keyword.cloud_notm}}-Endpunkten. Dieser Wert ist zum Festlegen der API-Endpunkte erforderlich.
   </dd>

<dt><code>--insecure</code></dt>
<dd>Lässt eine unsichere HTTP-Verbindung zu. Dieses Flag ist optional.</dd>

<dt><code>--skip-ssl-validation</code></dt>
<dd>Lässt unsichere SSL-Zertifikate zu. Dieses Flag ist optional.</dd>

<dt><code>--api-version WERT</code></dt>
<dd>Gibt die API-Version des Service an, den Sie verwenden möchten. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>

</dl>

**Beispiel**: Zeigen Sie Informationen zu dem aktuellen Endpunkt an, der als Ziel angegeben wurde.
```
ibmcloud ks api
```
{: pre}

```
API Endpoint:          https://containers.cloud.ibm.com
API Version:           v1
Skip SSL Validation:   false
Region:                us-south
```
{: screen}

</br>
### `ibmcloud ks apiserver-refresh (cluster-refresh)`
{: #cs_apiserver_refresh}

Wendet Konfigurationsänderungen für den Kubernetes-Master an, die mit den Befehlen `ibmcloud ks apiserver-config-set`, `apiserver-config-unset`, `cluster-feature-enable` oder `cluster-feature-disable` angefordert wurden. Die hoch verfügbaren Kubernetes-Masterkomponenten werden über einen rollierenden Neustart erneut gestartet. Die Workerknoten, Apps und Ressourcen werden nicht geändert und weiterhin ausgeführt.
{: shortdesc}



```
ibmcloud ks apiserver-refresh --cluster CLUSTER [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

<br />


## Befehle für die Verwendung des CLI-Plug-ins
{: #cli_plug-in_commands}

### `ibmcloud ks help`
{: #cs_help}

Zeigt eine Liste der unterstützten Befehle und Parameter an.
{: shortdesc}

```
ibmcloud ks help
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen:** Keine

</br>
### `ibmcloud ks init`
{: #cs_init}

Initialisiert das {{site.data.keyword.containerlong_notm}}-Plug-in oder gibt die Region an, in der Sie Kubernetes-Cluster erstellen oder darauf zugreifen möchten.
{: shortdesc}

Regionsspezifische Endpunkte werden nicht mehr verwendet. Verwenden Sie stattdessen den [globalen Endpunkt](/docs/containers?topic=containers-regions-and-zones#endpoint). Wenn Sie regionale Endpunkte verwenden müssen, [setzen Sie die Umgebungsvariable `IKS_BETA_VERSION` im {{site.data.keyword.containerlong_notm}}-Plug-in auf `0.2`](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta).
{: deprecated}

Wenn Sie nur Ressourcen aus einer Region auflisten und mit ihnen arbeiten müssen, können Sie den Befehl `ibmcloud ks init` verwenden, um einen regionalen Endpunkt anstelle des globalen Endpunkts zu verwenden.

* Dallas (Vereinigte Staaten (Süden), us-south): `https://us-south.containers.cloud.ibm.com`
* Frankfurt (Mitteleuropa, eu-de): `https://eu-de.containers.cloud.ibm.com`
* London (Vereinigtes Königreich (Süden), eu-gb): `https://eu-gb.containers.cloud.ibm.com`
* Sydney (Asien-Pazifik (Süden), au-syd): `https://au-syd.containers.cloud.ibm.com`
* Tokio (Asien-Pazifik (Norden), jp-tok): `https://jp-tok.containers.cloud.ibm.com`
* Washington, D.C. (Vereinigte Staaten (Osten), us-east): `https://us-east.containers.cloud.ibm.com`

Um die globale Funktionalität zu verwenden, können Sie den Befehl `ibmcloud ks init` erneut verwenden, um den globalen Endpunkt als Ziel festzulegen: `https://containers.cloud.ibm.com`

```
ibmcloud ks init [--host HOST] [--insecure] [-p] [-u] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen**:
<dl>
<dt><code>--host <em>HOST</em></code></dt>
<dd>Der zu verwendende {{site.data.keyword.containerlong_notm}}-API-Endpunkt. Dieser Wert ist optional.</dd>

<dt><code>--insecure</code></dt>
<dd>Lässt eine unsichere HTTP-Verbindung zu.</dd>

<dt><code>-p</code></dt>
<dd>Ihr IBM Cloud-Kennwort.</dd>

<dt><code>-u</code></dt>
<dd>Ihr IBM Cloud-Benutzername.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>

</dl>

**Beispiele**:
*  Beispiel für das Festlegen des regionalen Endpunkts "Vereinigte Staaten (Süden)":
  ```
  ibmcloud ks init --host https://us-south.containers.cloud.ibm.com
  ```
  {: pre}
*  Beispiel für das erneute Festlegen des globalen Endpunkts:
  ```
  ibmcloud ks init --host https://containers.cloud.ibm.com
  ```
  {: pre}
</br>

### `ibmcloud ks messages`
{: #cs_messages}

Zeigt aktuelle Nachrichten vom {{site.data.keyword.containerlong_notm}}-CLI-Plug-in für den Benutzer der IBMid an.
{: shortdesc}

```
ibmcloud ks messages
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

<br />


## Clusterbefehle: Management
{: #cluster_mgmt_commands}

### `ibmcloud ks addon-versions`
{: #cs_addon_versions}

Liste der Versionen anzeigen, die für verwaltete Add-ons in {{site.data.keyword.containerlong_notm}} unterstützt werden.
{: shortdesc}



```
ibmcloud ks addon-versions [--addon ADD-ON_NAME] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen**:
<dl>
<dt><code>--addon <em>ADD-ON_NAME</em></code></dt>
<dd>Optional: Geben Sie den Namen eines Add-ons ein, z. B. <code>istio</code> oder <code>knative</code>, für den nach Versionen gefiltert werden soll.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:

  ```
  ibmcloud ks addon-versions --addon istio
  ```
  {: pre}

</br>
### `ibmcloud ks cluster-addon-disable`
{: #cs_cluster_addon_disable}

Inaktiviert ein verwaltetes Add-on in einem vorhandenen Cluster. Dieser Befehl muss mit einem der folgenden Unterbefehle für das verwaltete Add-on kombiniert werden, das Sie inaktivieren möchten.
{: shortdesc}





#### `ibmcloud ks cluster-addon-disable istio`
{: #cs_cluster_addon_disable_istio}

Inaktiviert das verwaltete Istio-Add-on. Entfernt alle Istio-Kernkomponenten aus dem Cluster, einschließlich Prometheus.
{: shortdesc}

```
ibmcloud ks cluster-addon-disable istio --cluster CLUSTER [-f]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-f</code></dt>
<dd>Optional: Dieses Istio-Add-on ist eine Abhängigkeit für die verwalteten Add-ons <code>istio-extras</code>, <code>istio-sample-bookinfo</code> und <code>knative</code>. Schließen Sie dieses Flag ein, um auch diese Add-ons zu inaktivieren.</dd>
</dl>

#### `ibmcloud ks cluster-addon-disable istio-extras`
{: #cs_cluster_addon_disable_istio_extras}

Inaktiviert das verwaltete Istio-Extras-Add-on. Entfernt Grafana, Jeager und Kiali aus dem Cluster.
{: shortdesc}

```
ibmcloud ks cluster-addon-disable istio-extras --cluster CLUSTER [-f]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-f</code></dt>
<dd>Optional: Dieses Istio-Add-on ist eine Abhängigkeit für das verwaltete Add-on <code>istio-sample-bookinfo</code>. Schließen Sie dieses Flag ein, um auch dieses Add-on zu inaktivieren.</dd>
</dl>

#### `ibmcloud ks cluster-addon-disable istio-sample-bookinfo`
{: #cs_cluster_addon_disable_istio_sample_bookinfo}

Inaktiviert das verwaltete Istio-BookInfo-Add-on. Entfernt alle Bereitstellungen, Pods und anderen BookInfo-App-Ressourcen aus dem Cluster.
{: shortdesc}

```
ibmcloud ks cluster-addon-disable istio-sample-bookinfo --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>
</dl>

#### `ibmcloud ks cluster-addon-disable knative`
{: #cs_cluster_addon_disable_knative}

Inaktiviert das verwaltete Knative-Add-on, um das serverunabhängige Knative-Framework aus dem Cluster zu entfernen.
{: shortdesc}

```
ibmcloud ks cluster-addon-disable knative --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>
</dl>

#### `ibmcloud ks cluster-addon-disable kube-terminal`
{: #cs_cluster_addon_disable_kube-terminal}

Inaktivieren Sie das [Kubernetes-Terminal](/docs/containers?topic=containers-cs_cli_install#cli_web)-Add-on. Um das Kubernetes-Terminal in der Konsole des {{site.data.keyword.containerlong_notm}}-Clusters zu verwenden, müssen Sie zuerst das Add-on wieder aktivieren.
{: shortdesc}

```
ibmcloud ks cluster-addon-disable kube-terminal --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>
</dl>

</br>

### `ibmcloud ks cluster-addon-enable`
{: #cs_cluster_addon_enable}

Aktiviert ein verwaltetes Add-on in einem vorhandenen Cluster. Dieser Befehl muss mit einem der folgenden Unterbefehle für das verwaltete Add-on kombiniert werden, das Sie aktivieren möchten.
{: shortdesc}





#### `ibmcloud ks cluster-addon-enable istio`
{: #cs_cluster_addon_enable_istio}

Aktiviert das verwaltete [Istio-Add-on](/docs/containers?topic=containers-istio). Installiert die Kernkomponenten von Istio, einschließlich Prometheus.
{: shortdesc}

```
ibmcloud ks cluster-addon-enable istio --cluster CLUSTER [--version VERSION]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Optional: Geben Sie die Version des Add-ons an, das installiert werden soll. Ist keine Version angegeben, wird die Standardversion installiert.</dd>
</dl>

#### `ibmcloud ks cluster-addon-enable istio-extras`
{: #cs_cluster_addon_enable_istio_extras}

Aktiviert das verwaltete Istio-Extras-Add-on. Installiert Grafana, Jeager und Kiali, um zusätzliche Überwachungs-, Tracing- und Visualisierungsfunktionen für Istio bereitzustellen.
{: shortdesc}

```
ibmcloud ks cluster-addon-enable istio-extras --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Optional: Geben Sie die Version des Add-ons an, das installiert werden soll. Ist keine Version angegeben, wird die Standardversion installiert.</dd>

<dt><code>-y</code></dt>
<dd>Optional: Aktiviert die Add-on-Abhängigkeit <code>istio</code>.</dd>
</dl>

#### `ibmcloud ks cluster-addon-enable istio-sample-bookinfo`
{: #cs_cluster_addon_enable_istio_sample_bookinfo}

Aktiviert das verwaltete Istio-BookInfo-Add-on. Stellt die [Beispielanwendung BookInfo für Istio ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://istio.io/docs/examples/bookinfo/) im Standardnamensbereich (<code>default</code>) bereit.
{: shortdesc}

```
ibmcloud ks cluster-addon-enable istio-sample-bookinfo --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Optional: Geben Sie die Version des Add-ons an, das installiert werden soll. Ist keine Version angegeben, wird die Standardversion installiert.</dd>

<dt><code>-y</code></dt>
<dd>Optional: Aktiviert die Add-on-Abhängigkeiten <code>istio</code> und <code>istio-extras</code>.</dd>
</dl>

#### `ibmcloud ks cluster-addon-enable knative`
{: #cs_cluster_addon_enable_knative}

Aktiviert das verwaltete [Knative-Add-on](/docs/containers?topic=containers-serverless-apps-knative), um das serverunabhängige Knative-Framework zu installieren.
{: shortdesc}

```
ibmcloud ks cluster-addon-enable knative --cluster CLUSTER [--version VERSION] [-y]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Optional: Geben Sie die Version des Add-ons an, das installiert werden soll. Ist keine Version angegeben, wird die Standardversion installiert.</dd>

<dt><code>-y</code></dt>
<dd>Optional: Aktiviert die Add-on-Abhängigkeit <code>istio</code>.</dd>
</dl>

#### `ibmcloud ks cluster-addon-enable kube-terminal`
{: #cs_cluster_addon_enable_kube-terminal}

Aktivieren Sie das [Kubernetes-Terminal](/docs/containers?topic=containers-cs_cli_install#cli_web)-Add-on, um das Kubernetes-Terminal in der Konsole des {{site.data.keyword.containerlong_notm}}-Clusters zu verwenden.
{: shortdesc}

```
ibmcloud ks cluster-addon-enable kube-terminal --cluster CLUSTER [--version VERSION]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--version <em>VERSION</em></code></dt>
<dd>Optional: Geben Sie die Version des Add-ons an, das installiert werden soll. Ist keine Version angegeben, wird die Standardversion installiert.</dd>
</dl>
</br>

### `ibmcloud ks cluster-addons`
{: #cs_cluster_addons}

Listet verwaltete Add-ons auf, die in einem Cluster aktiviert sind.
{: shortdesc}



```
ibmcloud ks cluster-addons --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>
</dl>


</br>

### `ibmcloud ks cluster-config`
{: #cs_cluster_config}

Laden Sie nach erfolgter Anmeldung Kubernetes-Konfigurationsdaten und -Zertifikate herunter, um eine Verbindung zum Cluster herzustellen und `kubectl`-Befehle auszuführen. Die Dateien werden in `ausgangsverzeichnis_des_benutzers/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>` heruntergeladen.
{: shortdesc}



```
ibmcloud ks cluster-config --cluster CLUSTER [--admin] [--export] [--network] [--powershell] [--skip-rbac] [-s] [--yaml]
```
{: pre}

**Erforderliche Mindestberechtigungen:** {{site.data.keyword.cloud_notm}} IAM-Servicerolle **Anzeigeberechtigter** oder **Leseberechtigter** für den Cluster in {{site.data.keyword.containerlong_notm}}. Wenn Sie nur über eine Plattformrolle oder eine Servicerolle verfügen, gelten zusätzliche Einschränkungen.
* **Plattform:** Wenn Sie nur über eine Plattformrolle verfügen, können Sie diesen Befehl ausführen, jedoch benötigen Sie eine [Servicerolle](/docs/containers?topic=containers-users#platform) oder eine [angepasste RBAC-Richtlinie](/docs/containers?topic=containers-users#role-binding), um Kubernetes-Aktionen in dem Cluster auszuführen.
* **Service:** Wenn Sie nur über eine Servicerolle verfügen, können Sie diesen Befehl ausführen. Ihr Clusteradministrator muss Ihnen jedoch den Clusternamen und die Cluster-ID geben, weil Sie weder den Befehl `ibmcloud ks clusters` ausführen können, noch die {{site.data.keyword.containerlong_notm}}-Konsole starten können, um Cluster anzuzeigen. Nachdem Sie den Clusternamen und die ID erhalten haben, können Sie das [Kubernetes-Dashboard über die CLI starten](/docs/containers?topic=containers-app#db_cli) und mit Kubernetes arbeiten.

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--admin</code></dt>
<dd>Lädt die TLS-Zertifikate und die entsprechenden Berechtigungsdateien für die Rolle 'Superuser' herunter. Sie können die Zertifikate verwenden, um Tasks in einem Cluster zu automatisieren, ohne eine erneute Authentifizierung durchführen zu müssen. Die Dateien werden in  `<user_home_directory>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>-admin` heruntergeladen. Dieser Wert ist optional.</dd>

<dt><code>--network</code></dt>
<dd>Lädt die Calico-Konfigurationsdatei, die TLS-Zertifikate und die Berechtigungsdateien herunter, die für die Ausführung von <code>calicoctl</code>-Befehlen im Cluster erforderlich sind. Dieser Wert ist optional. **Hinweis:** Zum Abrufen des Exportbefehls für das Herunterladen der Kubernetes-Konfigurationsdaten und -Zertifikate müssen Sie diesen Befehl ohne dieses Flag ausführen.</dd>

<dt><code>--export</code></dt>
<dd>Lädt die Kubernetes-Konfigurationsdaten und -Zertifikate ohne Nachrichten außer dem Exportbefehl herunter. Da keine Nachrichten angezeigt werden, können Sie dieses Flag verwenden, wenn Sie automatisierte Scripts erstellen. Dieser Wert ist optional.</dd>

<dt><code>--powershell</code></dt>
<dd>Ruft Umgebungsvariablen im Windows-PowerShell-Format ab.</dd>

<dt><code>--skip-rbac</code></dt>
<dd>Überspringt das Hinzufügen von RBAC-Benutzerrollen für Kubernetes auf Basis der {{site.data.keyword.cloud_notm}} IAM-Servicezugriffsrollen zur Clusterkonfiguration. Schließen Sie diese Option nur ein, wenn Sie [eigene RBAC-Rollen für Kubernetes verwalten](/docs/containers?topic=containers-users#rbac). Wenn Sie alle Ihre RBAC-Benutzer mit [{{site.data.keyword.cloud_notm}} IAM-Servicezugriffsrollen](/docs/containers?topic=containers-access_reference#service) verwalten, geben Sie diese Option nicht an.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>

<dt><code>--yaml</code></dt>
<dd>Druckt die Befehlsausgabe im YAML-Format. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-config --cluster mein_cluster
```
{: pre}

</br>
### `ibmcloud ks cluster-create`
{: #cs_cluster_create}

Erstellt einen Cluster in Ihrer Organisation. Für kostenlose Cluster geben Sie den Clusternamen an. Alle anderen Angaben werden auf Standardwerte gesetzt. Ein kostenloser Cluster wird nach 30 Tagen automatisch gelöscht. Sie können zu einem Zeitpunkt jeweils nur über einen kostenlosen Cluster verfügen. Wenn Sie die volle Funktionalität von Kubernetes nutzen möchten, erstellen Sie einen Standardcluster.
{: shortdesc}



```
ibmcloud ks cluster-create [--file DATEIPOSITION] [--hardware HARDWARE] --zone ZONE --machine-type MASCHINENTYP --name NAME [--kube-version MAJOR.MINOR.PATCH] [--no-subnet] [--private-vlan PRIVATES_VLAN] [--public-vlan ÖFFENTLICHES_VLAN] [--private-only] [--private-service-endpoint] [--public-service-endpoint] [--workers WORKER] [--disable-disk-encrypt] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:**
* Die Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}} auf Kontoebene
* Die Plattformrolle **Administrator** für {{site.data.keyword.registrylong_notm}} auf Kontoebene
* Die Rolle **Superuser** für die IBM Cloud-Infrastruktur

**Befehlsoptionen**

<dl>
<dt><code>--file <em>DATEIPOSITION</em></code></dt>

<dd>Der Pfad zur YAML-Datei für die Erstellung Ihres Standardclusters. Statt die Merkmale Ihres Clusters mithilfe der in diesem Befehl bereitgestellten Optionen zu definieren, können Sie eine YAML-Datei verwenden. Dieser Wert ist für Standardcluster optional und steht für kostenlose Cluster nicht zur Verfügung. <p class="note">Wenn Sie dieselbe Option wie im Befehl als Parameter in der YAML-Datei bereitstellen, hat der Wert im Befehl Vorrang vor dem Wert in der YAML. Wenn Sie z. B. eine Position in Ihrer YAML-Datei definieren und die Option <code>--zone</code> im Befehl verwenden, überschreibt der Wert, den Sie in die Befehlsoption eingegeben haben, den Wert in der YAML-Datei.</p>
<pre class="codeblock">
<code>name: <em>&lt;clustername&gt;</em>
zone: <em>&lt;zone&gt;</em>
no-subnet: <em>&lt;kein_teilnetz&gt;</em>
machine-type: <em>&lt;maschinentyp&gt;</em>
private-vlan: <em>&lt;privates_vlan&gt;</em>
public-vlan: <em>&lt;öffentliches_vlan&gt;</em>
private-service-endpoint: <em>&lt;true&gt;</em>
public-service-endpoint: <em>&lt;true&gt;</em>
hardware: <em>&lt;shared_oder_dedicated&gt;</em>
workerNum: <em>&lt;anzahl_worker&gt;</em>
kube-version: <em>&lt;kube-version&gt;</em>
diskEncryption: <em>false</em>
</code></pre>
</dd>

<dt><code>--hardware <em>HARDWARE</em></code></dt>
<dd>Der Grad an Hardware-Isolation für Ihren Workerknoten. Verwenden Sie `dedicated`, wenn die verfügbaren physischen Ressourcen nur Ihnen zugeordnet werden sollen, oder `shared`, um zuzulassen, dass physische Ressourcen mit anderen IBM Kunden gemeinsam genutzt werden können. Die Standardeinstellung ist `shared`. Dieser Wert ist für VM-Standardcluster optional und steht für kostenlose Cluster nicht zur Verfügung. Geben Sie für Bare-Metal-Tyen `dedicated` an. </dd>

<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Die Zone, in der der Cluster erstellt werden soll. Dieser Wert ist für Standardcluster erforderlich. Kostenlose Cluster können in der Region erstellt werden, die Sie mit dem Befehl <code>ibmcloud ks region-set</code> als Ziel festgelegt haben; die Zone können Sie jedoch nicht angeben.

<p>Überprüfen Sie die [verfügbaren Zonen](/docs/containers?topic=containers-regions-and-zones#zones). Damit sich Ihr Cluster über Zonen erstreckt, müssen Sie den Cluster in einer [mehrzonenfähigen Zone](/docs/containers?topic=containers-regions-and-zones#zones) erstellen.</p>

<p class="note">Wenn Sie eine Zone auswählen, die sich außerhalb Ihres Landes befindet, müssen Sie daran denken, dass Sie möglicherweise eine Berechtigung benötigen, bevor Daten physisch in einem fremden Land gespeichert werden können.</p>
</dd>

<dt><code>--machine-type <em>MASCHINENTYP</em></code></dt>
<dd>Wählen Sie für Ihre Workerknoten einen Typ oder Maschinentyp aus. Sie können Ihre Workerknoten als virtuelle Maschinen auf gemeinsam genutzter oder dedizierter Hardware oder als physische Maschinen auf Bare-Metal-Systemen bereitstellen. Die Typen der verfügbaren physischen und virtuellen Maschinen variieren je nach der Zone, in der Sie den Cluster bereitstellen. Weitere Informationen finden Sie in der Dokumentation zum [Befehl](#cs_machine_types) `ibmcloud ks flavors (machine-types)`. Dieser Wert ist für Standardcluster erforderlich und steht für kostenlose Cluster nicht zur Verfügung.</dd>

<dt><code>--name <em>NAME</em></code></dt>
<dd>Der Name für den Cluster. Dieser Wert ist erforderlich. Der Name muss mit einem Buchstaben beginnen, darf Buchstaben, Ziffern und den Bindestrich (-) enthalten und darf maximal 35 Zeichen lang sein. Verwenden Sie einen Namen, der in allen Regionen eindeutig ist. Der vollständig qualifizierte Domänenname für die Ingress-Unterdomäne setzt sich aus dem Clusternamen und der Region zusammen, in der der Cluster bereitgestellt wird. Um sicherzustellen, dass die Ingress-Unterdomäne innerhalb einer Region eindeutig ist, wird der Clustername möglicherweise abgeschnitten und es wird ein beliebiger Wert innerhalb des Ingress-Domänennamens angehängt.
</dd>

<dt><code>--kube-version <em>MAJOR.MINOR.PATCH</em></code></dt>
<dd>Die Kubernetes-Version für den Cluster-Masterknoten. Dieser Wert ist optional. Wenn die Version nicht angegeben ist, wird der Cluster mit dem Standard für unterstützte Kubernetes-Versionen erstellt. Führen Sie den Befehl <code>ibmcloud ks versions</code> aus, um die verfügbaren Versionen anzuzeigen.</dd>

<dt><code>--no-subnet</code></dt>
<dd>Standardmäßig werden sowohl ein öffentliches als auch ein privates portierbares Teilnetz in dem VLAN erstellt, das dem Cluster zugeordnet ist. Schließen Sie das Flag <code>--no-subnet</code> ein, um zu verhindern, dass Teilnetze für den Cluster erstellt werden. Sie können Teilnetze zu einem späteren Zeitpunkt [erstellen](#cs_cluster_subnet_create) oder zu einem Cluster [hinzufügen](#cs_cluster_subnet_add).</dd>

<dt><code>--private-vlan <em>PRIVATES_VLAN</em></code></dt>
<dd>
<ul>
<li>Dieser Parameter ist für kostenlose Cluster nicht verfügbar.</li>
<li>Wenn es sich bei diesem Standardcluster um den ersten Standardcluster handelt, den Sie in dieser Zone erstellen, schließen Sie dieses Flag nicht ein. Ein privates VLAN wird zusammen mit dem Cluster für Sie erstellt.</li>
<li>Wenn Sie bereits einen Standardcluster in dieser Zone oder ein privates VLAN in der IBM Cloud-Infrastruktur erstellt haben, müssen Sie dieses private VLAN angeben. Private VLAN-Router beginnen immer mit <code>bcr</code> (Back-End-Router) und öffentliche VLAN-Router immer mit <code>fcr</code> (Front-End-Router). Wenn Sie einen Cluster erstellen und die öffentlichen und privaten VLANs angeben, muss die Zahlen- und Buchstabenkombination nach diesen Präfixen übereinstimmen. </li>
</ul>
<p>Führen Sie <code>ibmcloud ks vlans --zone <em>&lt;zone&gt;</em></code> aus, um herauszufinden, ob Sie bereits über ein privates VLAN für eine bestimmte Zone verfügen, oder um den Namen eines vorhandenen privaten VLANs zu erfahren.</p></dd>

<dt><code>--public-vlan <em>ÖFFENTLICHES_VLAN</em></code></dt>
<dd>
<ul>
<li>Dieser Parameter ist für kostenlose Cluster nicht verfügbar.</li>
<li>Wenn es sich bei diesem Standardcluster um den ersten Standardcluster handelt, den Sie in dieser Zone erstellen, verwenden Sie dieses Flag nicht. Ein öffentliches VLAN wird zusammen mit dem Cluster für Sie erstellt.</li>
<li>Wenn Sie bereits einen Standardcluster in dieser Zone oder ein öffentliches VLAN in der IBM Cloud-Infrastruktur erstellt haben, geben Sie dieses öffentliche VLAN an. Wenn Sie Ihre Workerknoten nur mit einem private VLAN verbinden möchten, geben Sie diese Option nicht an. Private VLAN-Router beginnen immer mit <code>bcr</code> (Back-End-Router) und öffentliche VLAN-Router immer mit <code>fcr</code> (Front-End-Router). Wenn Sie einen Cluster erstellen und die öffentlichen und privaten VLANs angeben, muss die Zahlen- und Buchstabenkombination nach diesen Präfixen übereinstimmen. </li>
</ul>

<p>Führen Sie <code>ibmcloud ks vlans --zone <em>&lt;zone&gt;</em></code> aus, um herauszufinden, ob Sie bereits über ein öffentliches VLAN für eine bestimmte Zone verfügen, oder um den Namen eines vorhandenen öffentlichen VLANs zu erfahren.</p></dd>

<dt><code>--private-only </code></dt>
<dd>Verwenden Sie diese Option, um zu verhindern, dass ein öffentliches VLAN erstellt wird. Dieser Wert ist nur erforderlich, wenn Sie das Flag `--private-vlan` angeben und das Flag `--public-vlan` nicht einschließen.<p class="note">Wenn Workerknoten nur mit einem privaten VLAN eingerichtet werden, müssen Sie den privaten Serviceendpunkt aktivieren oder eine Gateway-Einheit konfigurieren. Weitere Informationen finden Sie unter [Worker-zu-Master- und Benutzer-zu-Master-Kommmunikation](/docs/containers?topic=containers-plan_clusters#workeruser-master).</p></dd>

<dt><code>--private-service-endpoint</code></dt>
<dd>**Standardcluster mit Kubernetes Version 1.11 oder höher in [VRF-aktivierten Konten](/docs/resources?topic=resources-private-network-endpoints#getting-started)**: Aktivieren Sie den [privaten Serviceendpunkt](/docs/containers?topic=containers-plan_clusters#workeruser-master), sodass Ihr Kubernetes-Master und die Workerknoten über das private VLAN kommunizieren können. Darüber hinaus können Sie den öffentlichen Serviceendpunkt mit dem Flag `--public-service-endpoint` aktivieren, um auf Ihren Cluster über das Internet zugreifen zu können. Wenn Sie nur den privaten Serviceendpunkt aktivieren, müssen Sie mit dem privaten VLAN verbunden sein, um mit Ihrem Kubernetes-Master zu kommunizieren. Nach dem Aktivieren eines privaten Serviceendpunkts können Sie diesen später nicht mehr inaktivieren.<br><br>Nach dem Erstellen des Clusters können Sie den Endpunkt mit dem Befehl `ibmcloud ks cluster-get --cluster <clustername_oder_-id>` abrufen.</dd>

<dt><code>--public-service-endpoint</code></dt>
<dd>**Standardcluster mit Kubernetes Version 1.11 oder höher**: Aktivieren Sie den [öffentlichen Serviceendpunkt](/docs/containers?topic=containers-plan_clusters#workeruser-master), sodass auf Ihren Kubernetes-Master über das öffentliche Netz zugegriffen werden kann, zum Beispiel um `kubectl`-Befehle über Ihr Terminal auszuführen. Wenn Sie ein [VRF-aktiviertes Konto](/docs/resources?topic=resources-private-network-endpoints#getting-started) haben und zusätzlich das Flag `--private-service-endpoint` angeben, erfolgt die Kommunikation zwischen Master und Workerknoten über das private und das öffentliche Netz. Sie können den öffentlichen Serviceendpunkt später inaktivieren, wenn Sie einen rein privaten Cluster wünschen.<br><br>Nach dem Erstellen des Clusters können Sie den Endpunkt mit dem Befehl `ibmcloud ks cluster-get --cluster <clustername_oder_-id>` abrufen.</dd>

<dt><code>--workers WORKER</code></dt>
<dd>Die Anzahl von Workerknoten, die Sie in Ihrem Cluster bereitstellen wollen. Wenn Sie diese Option nicht angeben, wird ein Cluster mit einem (1) Workerknoten erstellt. Dieser Wert ist für Standardcluster optional und steht für kostenlose Cluster nicht zur Verfügung.
<p class="important">Wenn Sie einen Cluster mit nur einem Workerknoten pro Zone erstellen, treten möglicherweise Probleme mit Ingress auf. Für Hochverfügbarkeit erstellen Sie einen Cluster mit mindestens zwei Workern pro Zone.</br></br>Jedem Workerknoten werden eine eindeutige Workerknoten-ID und ein Domänenname zugewiesen, die nach der Erstellung des Clusters nicht manuell geändert werden dürfen. Wenn die ID oder der Domänenname geändert wird, kann der Kubernetes-Master Ihren Cluster nicht mehr verwalten.</p></dd>

<dt><code>--disable-disk-encrypt</code></dt>
<dd>Workerknoten verfügen standardmäßig über eine 256-Bit-AES-Plattenverschlüsselung. [Weitere Informationen finden Sie hier](/docs/containers?topic=containers-security#encrypted_disk). Wenn Sie die Verschlüsselung inaktivieren möchten, schließen Sie diese Option ein.</dd>
</dl>



**<code>-s</code>**</br>
Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.

**Beispiele**:


**Kostenlosen Cluster erstellen**: Geben Sie nur den Clusternamen an; alles andere ist auf einen Standardwert gesetzt. Ein kostenloser Cluster wird nach 30 Tagen automatisch gelöscht. Sie können zu einem Zeitpunkt jeweils nur über einen kostenlosen Cluster verfügen. Wenn Sie die volle Funktionalität von Kubernetes nutzen möchten, erstellen Sie einen Standardcluster.

```
ibmcloud ks cluster-create --name mein_cluster
```
{: pre}

**Den ersten Standardcluster erstellen**: Für den ersten Standardcluster, der in einer Zone erstellt wird, wird auch ein privates VLAN erstellt. Schließen Sie daher nicht das Flag `--public-vlan` ein.
{: #example_cluster_create}

```
ibmcloud ks cluster-create --zone dal10 --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --name my_cluster --hardware shared --workers 2
```
{: pre}

**Nachfolgende Standardcluster erstellen**: Wenn Sie bereits einen Standardcluster in dieser Zone oder ein öffentliches VLAN in der IBM Cloud-Infrastruktur erstellt haben, geben Sie dieses öffentliche VLAN mit dem Flag `--public-vlan` an. Führen Sie `ibmcloud ks vlans --zone <zone>` aus, um herauszufinden, ob Sie bereits über ein öffentliches VLAN für eine bestimmte Zone verfügen, oder um den Namen eines vorhandenen öffentlichen VLANs zu erfahren.

```
ibmcloud ks cluster-create --zone dal10 --public-vlan my_public_VLAN_ID --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --name my_cluster --hardware shared --workers 2
```
{: pre}

</br>

### `ibmcloud ks cluster-feature-disable public-service-endpoint`
{: #cs_cluster_feature_disable}

Inaktivieren Sie den öffentlichen Serviceendpunkt für einen Cluster.
{: shortdesc}



**Wichtig**: Bevor Sie den öffentlichen Endpunkt inaktivieren, müssen Sie zuerst die folgenden Schritte ausführen, um den privaten Serviceendpunkt zu aktivieren:
1. Aktivieren Sie den privaten Serviceendpunkt mit dem Befehl `ibmcloud ks cluster-feature-enable private-service-endpoint --cluster <clustername>`.
2. Befolgen Sie die Eingabeaufforderungen in der CLI, um den API-Server für den Kubernetes-Master zu aktualisieren.
3. [Laden Sie alle Workerknoten neu in Ihren Cluster, um die Konfiguration des privaten Endpunkts aufzunehmen.](#cs_worker_reload)

```
ibmcloud ks cluster-feature-disable public-service-endpoint --cluster CLUSTER [-s] [-f]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-feature-disable public-service-endpoint --cluster mein_cluster
```
{: pre}

</br>
### `ibmcloud ks cluster-feature-enable`
{: #cs_cluster_feature_enable}

Aktiviert eine Funktion auf einem vorhandenen Cluster. Dieser Befehl muss mit einem der folgenden Unterbefehle für die Funktion kombiniert werden, die Sie aktivieren möchten.
{: shortdesc}



#### `ibmcloud ks cluster-feature-enable private-service-endpoint`
{: #cs_cluster_feature_enable_private_service_endpoint}

Aktiviert den [privaten Serviceendpunkt](/docs/containers?topic=containers-plan_clusters#workeruser-master), um Ihren Cluster-Master privat zugänglich zu machen.
{: shortdesc}

Gehen Sie wie folgt vor, um diesen Befehl auszuführen:
1. Aktivieren Sie [VRF](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) in Ihrem Konto für die IBM Cloud-Infrastruktur. Wenn Sie prüfen wollen, ob VRF bereits aktiviert wurde, dann verwenden Sie den Befehl `ibmcloud account show`. 
2. [Aktivieren Sie Ihr {{site.data.keyword.cloud_notm}}-Konto zur Verwendung von Serviceendpunkten](/docs/resources?topic=resources-private-network-endpoints#getting-started).
3. Führen Sie den Befehl `ibmcloud ks cluster-feature-enable private-service-endpoint --cluster <clustername>` aus.
4. Befolgen Sie die Eingabeaufforderungen in der CLI, um den API-Server für den Kubernetes-Master zu aktualisieren.
5. [Laden Sie alle Workerknoten neu](#cs_worker_reload) in Ihren Cluster, um die Konfiguration des privaten Endpunkts aufzunehmen.

```
ibmcloud ks cluster-feature-enable private-service-endpoint --cluster CLUSTER [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-feature-enable private-service-endpoint --cluster mein_cluster
```
{: pre}

#### `ibmcloud ks cluster-feature-enable public-service-endpoint`
{: #cs_cluster_feature_enable_public_service_endpoint}

Aktiviert den [öffentlichen Serviceendpunkt](/docs/containers?topic=containers-plan_clusters#workeruser-master), um Ihren Cluster-Master öffentlich zugänglich zu machen.
{: shortdesc}

Nach Ausführung dieses Befehls müssen Sie den API-Server für die Verwendung des Serviceendpunkts aktualisieren, indem Sie die Eingabeaufforderungen in der CLI befolgen.

```
ibmcloud ks cluster-feature-enable public-service-endpoint --cluster CLUSTER [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-feature-enable public-service-endpoint --cluster mein_cluster
```
{: pre}

</br>
### `ibmcloud ks cluster-get`
{: #cs_cluster_get}

Details eines Clusters anzeigen.
{: shortdesc}



```
ibmcloud ks cluster-get --cluster CLUSTER [--json] [--showResources] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code><em>--showResources</em></code></dt>
<dd>Weitere Clusterressourcen wie z. B. Add-ons, VLANs, Teilnetze und Speicher anzeigen.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-get --cluster mein_cluster --showResources
```
{: pre}

**Beispielausgabe**:
```
Name:                           mycluster
ID:                             df253b6025d64944ab99ed63bb4567b6
State:                          normal
Created:                        2018-09-28T15:43:15+0000
Location:                       dal10
Master URL:                     https://c3.<region>.containers.cloud.ibm.com:30426
Public Service Endpoint URL:    https://c3.<region>.containers.cloud.ibm.com:30426
Private Service Endpoint URL:   https://c3-private.<region>.containers.cloud.ibm.com:31140
Master Location:                Dallas
Master Status:                  Ready (21 hours ago)
Ingress Subdomain:              mycluster.us-south.containers.appdomain.cloud
Ingress Secret:                 mycluster
Workers:                        6
Worker Zones:                   dal10, dal12
Version:                        1.11.3_1524
Owner:                          owner@email.com
Resource Group ID:              a8a12accd63b437bbd6d58fb6a462ca7
Resource Group Name:            Default

Subnet VLANs
VLAN ID   Subnet CIDR         Public   User-managed
2234947   10.xxx.xx.xxx/29    false    false
2234945   169.xx.xxx.xxx/29  true    false

```
{: screen}

</br>
### `ibmcloud ks cluster-pull-secret-apply`
{: #cs_cluster_pull_secret_apply}

Erstellt eine {{site.data.keyword.cloud_notm}} IAM-Service-ID für den Cluster, erstellt eine Richtlinie für die Service-ID, die die Servicezugriffsrolle **Leseberechtigter** in {{site.data.keyword.registrylong_notm}} zuordnet, und erstellt dann einen API-Schlüssel für die Service-ID. Der API-Schlüssel wird anschließend in einem geheimen Kubernetes-Schlüssel zum Extrahieren von Images (`imagePullSecret`) gespeichert, sodass Sie Images aus Ihren {{site.data.keyword.registryshort_notm}}-Namensbereichen für Container extrahieren können, die sich im Kubernetes-Standardnamensbereich (`default`) befinden. Dieser Prozess erfolgt automatisch, wenn Sie einen Cluster erstellen. Wenn beim Prozess der Clustererstellung ein Fehler auftritt oder wenn Sie einen vorhandenen Cluster haben, können Sie mit diesem Befehl den Prozess erneut anwenden.
{: shortdesc}

Diese API-Schlüsselmethode ersetzt die vorherige Methode der Berechtigung eines Clusters für den Zugriff auf {{site.data.keyword.registrylong_notm}} durch automatisches Erstellen eines [Tokens](/docs/services/Registry?topic=registry-registry_access#registry_tokens) und Speichern des Tokens in einem geheimen Schlüssel für Image-Pull-Operationen. Durch die Verwendung von IAM-API-Schlüsseln für den Zugriff auf {{site.data.keyword.registrylong_notm}} können Sie jetzt IAM-Richtlinien für die Service-ID anpassen, um den Zugriff auf Ihre Namensbereiche oder auf bestimmte Images einzuschränken. Sie können zum Beispiel die Service-ID-Richtlinien im geheimen Schlüssel für Pull-Operationen des Clusters so ändern, dass nur Images aus einer bestimmten Registry-Region oder einem bestimmten Namensbereich extrahiert werden. Bevor Sie IAM-Richtlinien anpassen können, müssen Sie die [{{site.data.keyword.cloud_notm}} IAM-Richtlinien für {{site.data.keyword.registrylong_notm}} aktivieren](/docs/services/Registry?topic=registry-user#existing_users).

Weitere Informationen finden Sie unter [Berechtigung des Clusters zum Extrahieren von Images aus {{site.data.keyword.registrylong_notm}}](/docs/containers?topic=containers-images#cluster_registry_auth).



<p class="important">Wenn Sie diesen Befehl ausführen, wird die Erstellung von IAM-Berechtigungsnachweisen und geheimen Schlüsseln für Image-Pull-Operationen eingeleitet, deren Ausführung einige Zeit dauern kann. Sie können Container, die ein Image aus {{site.data.keyword.registrylong_notm}}-Domänen `icr.io` extrahieren, erst bereitstellen, wenn die geheimen Schlüssel für Image-Pull-Operationen erstellt wurden. Zur Prüfung der geheimen Schlüssel für Image-Pull-Operationen führen Sie den Befehl `kubectl get secrets | grep icr` aus.</br></br>Wenn Sie einer vorhandenen Service-ID IAM-Richtlinien hinzugefügt haben, um z. B. den Zugriff auf eine regionale Registry einzuschränken, werden die Service-ID, die IAM-Richtlinien und der API-Schlüssel für den geheimen Schlüssel für Image-Pull-Operationen durch diesen Befehl zurückgesetzt.
</p>

```
ibmcloud ks cluster-pull-secret-apply --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:**
*  Plattformrolle **Operator oder Administrator** für den Cluster in {{site.data.keyword.containerlong_notm}}
*  Plattformrolle **Administrator** in {{site.data.keyword.registrylong_notm}}

**Befehlsoptionen**:

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>
</dl>

</br>

### `ibmcloud ks cluster-rm`
{: #cs_cluster_rm}

Entfernt einen Cluster aus der Organisation.
{: shortdesc}



```
ibmcloud ks cluster-rm --cluster CLUSTER [--force-delete-storage] [-f] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--force-delete-storage</code></dt>
<dd>Löscht den Cluster und alle persistenten Speicher, die der Cluster verwendet. **Achtung**: Wenn Sie dieses Flag einschließen, können die im Cluster gespeicherten Daten oder die zugehörigen Speicherinstanzen nicht wiederhergestellt werden. Dieser Wert ist optional.</dd>

<dt><code>-f</code></dt>
<dd>Geben Sie diese Option an, um das Entfernen eines Clusters ohne Benutzereingabeaufforderungen zu erzwingen. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-rm --cluster mein_cluster
```
{: pre}

</br>

### `ibmcloud ks cluster-update`
{: #cs_cluster_update}

Aktualisiert den Kubernetes-Master auf die API-Standardversion. Während der Aktualisierung können Sie weder auf den Cluster zugreifen noch Änderungen am Cluster vornehmen. Workerknoten, Apps und Ressourcen, die vom Benutzer bereitgestellt wurden, werden nicht geändert und weiterhin ausgeführt.
{: shortdesc}

Möglicherweise müssen Sie Ihre YAML-Dateien für zukünftige Bereitstellungen ändern. Lesen Sie die detaillierten Informationen in diesen [Releaseinformationen](/docs/containers?topic=containers-cs_versions).



```
ibmcloud ks cluster-update --cluster CLUSTER [--kube-version MAJOR.MINOR.PATCH] [--force-update] [-f] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--kube-version <em>MAJOR.MINOR.PATCH</em></code></dt>
<dd>Die Kubernetes-Version des Clusters. Wenn Sie keine Version angeben, wird der Kubernetes-Master auf die API-Standardversion aktualisiert. Führen Sie den Befehl [ibmcloud ks kube-versions](#cs_kube_versions) aus, um die verfügbaren Versionen anzuzeigen. Dieser Wert ist optional.</dd>

<dt><code>--force-update</code></dt>
<dd>Versuch einer Aktualisierung, selbst wenn die Änderung mehr als zwei Nebenversionen von der Workerknotenversion abweicht. Dieser Wert ist optional.</dd>

<dt><code>-f</code></dt>
<dd>Erzwingt die Ausführung des Befehls ohne Eingabeaufforderungen. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-update --cluster mein_cluster
```
{: pre}

</br>
### `ibmcloud ks clusters`
{: #cs_clusters}

Listet alle Cluster in Ihrem {{site.data.keyword.cloud_notm}}-Konto auf.
{: shortdesc}



Cluster an allen Standorten werden zurückgegeben. Schließen Sie das Flag `--locations` ein, um Cluster nach einem bestimmten Standort zu filtern. Wenn Sie beispielsweise Cluster nach der Metropole `dal` filtern, werden Mehrzonencluster in dieser Metropole und Einzelzonencluster in Rechenzentren (Zonen) innerhalb dieser Metropole zurückgegeben. Wenn Sie Cluster nach dem Rechenzentrum (Zone) `dal10` filtern, werden Mehrzonencluster mit einem Workerknoten in dieser Zone und Einzelzonencluster in dieser Zone zurückgegeben. Sie können einen Standort oder eine durch Kommas getrennte Liste mit Standorten übergeben.

Wenn Sie die Betaversion `0.2` (traditionell) des {{site.data.keyword.containerlong_notm}}-Plug-ins verwenden, werden nur Cluster aus der Region zurückgegeben, die Sie zurzeit als Ziel angegeben haben. Um zwischen Regionen zu wechseln, führen Sie den Befehl `ibmcloud ks region-set` aus.
{: deprecated}

```
ibmcloud ks clusters [--locations STANDORT] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--locations <em>STANDORT</em></code></dt>
<dd>Filtert Zonen nach einem bestimmten Standort oder nach einer Liste durch Kommas getrennter Standorte. Führen Sie den Befehl <code>ibmcloud ks supported-locations</code> aus, um die unterstützten Standorte anzuzeigen.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks clusters --locations ams03,wdc,ap
```
{: pre}

</br>
### Veraltet: `ibmcloud ks kube-versions`
{: #cs_kube_versions}

Zeigt eine Liste der Kubernetes-Versionen an, die in {{site.data.keyword.containerlong_notm}} unterstützt werden. Aktualisieren Sie den [Cluster-Master](#cs_cluster_update) und die [Workerknoten](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update) auf die Standardversion für die aktuellen und stabilen Leistungsmerkmale.
{: shortdesc}

Dieser Befehl wird nicht mehr verwendet. Verwenden Sie stattdessen den [Befehl `ibmcloud ks versions`](#cs_versions_command).
{: deprecated}

```
ibmcloud ks kube-versions [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen**:
<dl>
<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks kube-versions
```
{: pre}

</br>

### `ibmcloud ks versions`
{: #cs_versions_command}

Listet alle Containerplattformversionen auf, die für {{site.data.keyword.containerlong_notm}}-Cluster verfügbar sind. Aktualisieren Sie den [Cluster-Master](#cs_cluster_update) und die [Workerknoten](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update) auf die Standardversion für die aktuellen und stabilen Leistungsmerkmale.
{: shortdesc}



```
ibmcloud ks versions [--show-version PLATTFORM][--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen**:
<dl>
<dt><code>--show-version</code> <em>PLATTFORM</em></dt>
<dd>Zeigt nur die Versionen der angegebenen Containerplattform an. Unterstützte Werte sind <code>kubernetes</code> oder <code>openshift</code>.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks versions
```
{: pre}

<br />



## Clusterbefehle: Services und Integrationen
{: #cluster_services_commands}

### `ibmcloud ks cluster-service-bind`
{: #cs_cluster_service_bind}

Erstellt Serviceberechtigungsnachweise für einen {{site.data.keyword.cloud_notm}}-Service und speichert diese Berechtigungsnachweise in einem geheimen Kubernetes-Schlüssel in Ihrem Cluster. Um die verfügbaren {{site.data.keyword.cloud_notm}}-Services aus dem {{site.data.keyword.cloud_notm}}-Katalog anzuzeigen, führen Sie den Befehl `ibmcloud service offerings` aus. **Hinweis**: Sie können nur {{site.data.keyword.cloud_notm}}-Services hinzufügen, die die Verwendung von Serviceschlüsseln unterstützen.
{: shortdesc}

Weitere Informationen zur Servicebindung und zu den Services, die Sie Ihrem Cluster hinzufügen können, finden Sie unter [Services unter Verwendung der IBM Cloud-Service-Bindung hinzufügen](/docs/containers?topic=containers-service-binding).



```
ibmcloud ks cluster-service-bind --cluster CLUSTER --namespace KUBERNETES-NAMENSBEREICH --service SERVICEINSTANZ [--key SERVICEINSTANZSCHLÜSSEL] [--role IAM-SERVICEROLLE] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für den Cluster in {{site.data.keyword.containerlong_notm}} und die Cloud Foundry-Rolle **Entwickler**

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--key <em>SERVICEINSTANZSCHLÜSSEL</em></code></dt>
<dd>Der Name oder die GUID eines vorhandenen Serviceschlüssels. Dieser Wert ist optional. Wenn Sie den Befehl `service-binding` verwenden, werden neue Serviceberechtigungsnachweise automatisch für Ihre Serviceinstanz erstellt und der IAM-Servicezugriffsrolle **Schreibberechtigter** (Writer) für IAM-fähige Services zugeordnet. Wenn Sie einen vorhandenen Serviceschlüssel verwenden möchten, den Sie zuvor erstellt haben, verwenden Sie diese Option. Wenn Sie einen Serviceschlüssel definieren, können Sie die Option `--role` nicht zusätzlich festlegen, da Ihre Serviceschlüssel bereits mit einer bestimmten IAM-Servicezugriffsrolle erstellt werden.</dd>

<dt><code>--namespace <em>KUBERNETES-NAMENSBEREICH</em></code></dt>
<dd>Der Name des Kubernetes-Namensbereichs, in dem Sie den geheimen Kubernetes-Schlüssel für Ihre Serviceberechtigungsnachweise erstellen möchten. Dieser Wert ist erforderlich.</dd>

<dt><code>--service <em>SERVICEINSTANZ</em></code></dt>
<dd>Der Name der {{site.data.keyword.cloud_notm}}-Serviceinstanz, die Sie binden möchten. Zum Herausfinden des Namens führen Sie für Cloud-Foundry-Services den Befehl <code>ibmcloud service list</code> aus und für IAM-fähige Services den Befehl <code>ibmcloud resource service-instances</code>. Dieser Wert ist erforderlich. </dd>

<dt><code>--role <em>IAM-SERVICEROLLE</em></code></dt>
<dd>Die {{site.data.keyword.cloud_notm}} IAM-Rolle, die der Serviceschlüssel haben soll. Dieser Wert ist optional und kann nur für IAM-fähige Services verwendet werden. Wenn Sie diese Option nicht festlegen, werden Ihre Serviceberechtigungsnachweise automatisch erstellt und der IAM-Servicezugriffsrolle **Schreibberechtigter** (Writer) zugeordnet. Wenn Sie vorhandene Serviceschlüssel verwenden möchten und dazu die Option `--key` angeben, schließen Sie diese Option nicht ein.<br><br>
Zum Auflisten der für einen Service verfügbaren Rollen führen Sie den Befehl `ibmcloud iam roles --service <servicename>` aus. Der Servicename ist der Name des Service im Katalog, den Sie mit dem Befehl `ibmcloud catalog search` abrufen können.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-service-bind --cluster mein_cluster --namespace mein_namensbereich --service meine_serviceinstanz
```
{: pre}

</br>
### `ibmcloud ks cluster-service-unbind`
{: #cs_cluster_service_unbind}

Entfernen Sie einen {{site.data.keyword.cloud_notm}}-Service aus einem Cluster, indem Sie seine Kubernetes-Namensbereichsbindung aufheben.
{: shortdesc}



Wenn Sie einen {{site.data.keyword.cloud_notm}}-Service entfernen, werden die Serviceberechtigungsnachweise aus dem Cluster entfernt. Wenn ein Pod den Service noch verwendet, schlägt er fehl, weil die Serviceberechtigungsnachweise nicht gefunden werden können.
{: tip}

```
ibmcloud ks cluster-service-unbind --cluster CLUSTER --namespace KUBERNETES_NAMESPACE --service SERVICE_INSTANCE [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für den Cluster in {{site.data.keyword.containerlong_notm}} und die Cloud Foundry-Rolle **Entwickler**

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--namespace <em>KUBERNETES-NAMENSBEREICH</em></code></dt>
<dd>Der Name des Kubernetes-Namensbereichs. Dieser Wert ist erforderlich.</dd>

<dt><code>--service <em>SERVICEINSTANZ</em></code></dt>
<dd>Der Name der {{site.data.keyword.cloud_notm}}-Serviceinstanz, die Sie entfernen möchten. Führen Sie den Befehl `ibmcloud ks cluster-services --cluster <clustername_oder_-id>` aus, um den Namen der Serviceinstanz herauszufinden. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-service-unbind --cluster mein_cluster --namespace mein_namensbereich --service 8567221
```
{: pre}

</br>
### `ibmcloud ks cluster-services`
{: #cs_cluster_services}

Listet die Services auf, die an einen oder an alle Kubernetes-Namensbereiche in einem Cluster gebunden sind. Werden keine Optionen angegeben, werden die Services für den Standardnamensbereich angezeigt.
{: shortdesc}



```
ibmcloud ks cluster-services --cluster CLUSTER [--namespace KUBERNETES-NAMENSBEREICH] [--all-namespaces] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--namespace <em>KUBERNETES-NAMENSBEREICH</em></code>, <code>-n <em>KUBERNETES-NAMENSBEREICH</em></code></dt>
<dd>Schließen Sie die Services ein, die an einen bestimmten Namensbereich in einem Cluster gebunden sind. Dieser Wert ist optional.</dd>

<dt><code>--all-namespaces</code></dt>
<dd>Schließen Sie die Services ein, die an alle Namensbereiche in einem Cluster gebunden sind. Dieser Wert ist optional.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-services --cluster mein_cluster --namespace mein_namensbereich
```
{: pre}

</br>
### `ibmcloud ks va`
{: #cs_va}

Nachdem Sie [den Container-Scanner installiert haben](/docs/services/va?topic=va-va_index#va_install_container_scanner), sehen Sie sich einen detaillierten Bericht zur Schwachstellenanalyse für einen Container in Ihrem Cluster an.
{: shortdesc}



```
ibmcloud ks va --container CONTAINER-ID [--extended] [--vulnerabilities] [--configuration-issues] [--json]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Servicezugriffsrolle **Leseberechtigter** für {{site.data.keyword.registrylong_notm}}. **Hinweis**: Ordnen Sie keine Richtlinien für {{site.data.keyword.registryshort_notm}} auf Ressourcengruppenebene zu.

**Befehlsoptionen**:
<dl>
<dt><code>--container CONTAINER-ID</code></dt>
<dd><p>Die ID des Containers. Dieser Wert ist erforderlich.</p>
<p>Gehen Sie wie folgt vor, um nach der ID Ihres Containers zu suchen:<ol><li>[Richten Sie die Kubernetes-CLI auf Ihren Cluster aus](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).</li><li>Listen Sie Ihre Pods auf, indem Sie `kubectl get pods` ausführen.</li><li>Suchen Sie nach dem Feld **Container ID** in der Ausgabe des Befehls `kubectl describe pod <pod-name>`. Beispiel: `Container ID: containerd://1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15`.</li><li>Entfernen Sie das Präfix `containerd://` aus der ID, bevor Sie die Container-ID für den Befehl `ibmcloud ks va` verwenden. Beispiel: `1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15`.</li></ol></p></dd>

<dt><code>--extended</code></dt>
<dd><p>Erweitern Sie die Befehlsausgabe, um mehr Korrekturinformationen für anfällige Pakete anzuzeigen. Dieser Wert ist optional.</p>
<p>Standardmäßig enthalten die Scanergebnisse die ID, den Richtlinienstatus, die betroffenen Pakete und einen Lösungsvorschlag. Mit dem Flag `--extended` werden Informationen wie die Zusammenfassung, der Sicherheitshinweis für Anbieter und der Link zum offiziellen Hinweis hinzugefügt.</p></dd>

<dt><code>--vulnerabilities</code></dt>
<dd>Beschränken Sie die Befehlsausgabe so, dass nur Paketschwachstellen angezeigt werden. Dieser Wert ist optional. Sie können dieses Flag nicht verwenden, wenn Sie das Flag `--configuration-issues` verwenden.</dd>

<dt><code>--configuration-issues</code></dt>
<dd>Beschränken Sie die Befehlsausgabe so, dass nur Konfigurationsprobleme angezeigt werden. Dieser Wert ist optional. Sie können dieses Flag nicht verwenden, wenn Sie das Flag `--vulnerabilities` verwenden.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks va --container 1a11a1aa2b2b22223333c44444ccc555667d7dd777888e8ef99f1011121314g15 --extended --vulnerabilities --json
```
{: pre}

</br>
### Betaversion: `ibmcloud ks key-protect-enable`
{: #cs_key_protect}

Verschlüsselt geheime Kubernetes-Schlüssel mithilfe von [{{site.data.keyword.keymanagementservicefull}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/key-protect?topic=key-protect-getting-started-tutorial#getting-started-tutorial) als [KMS-Provider (KMS - Key Management Service)![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) im Cluster. Zum turnusmäßigen Wechseln eines Schlüssels in einem Cluster mit vorhandener Schlüsselverschlüsselung führen Sie diesen Befehl erneut und mit einer neuen Rootschlüssel-ID aus.
{: shortdesc}

Löschen Sie keine Rootschlüssel in Ihrer {{site.data.keyword.keymanagementserviceshort}}-Instanz. Löschen Sie keine Schlüssel, auch dann nicht, wenn Sie rotieren, um einen neuen Schlüssel zu verwenden. Wenn Sie einen Rootschlüssel löschen, können Sie auf die Daten in etcd oder Daten aus den geheimen Schlüsseln in Ihrem Cluster nicht mehr zugreifen oder diese entfernen.
{: important}



```
ibmcloud ks key-protect-enable --cluster CLUSTERNAME_ODER_-ID --key-protect-url ENDPUNKT --key-protect-instance GUID_DER_INSTANZ --crk ROOTSCHLÜSSEL-ID
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--container CLUSTERNAME_ODER_-ID</code></dt>
<dd>Der Name oder die ID des Clusters.</dd>

<dt><code>--key-protect-url ENDPUNKT</code></dt>
<dd>Der {{site.data.keyword.keymanagementserviceshort}}-Endpunkt für die Clusterinstanz. Informationen zum Abrufen des Endpunkts finden Sie unter [Serviceendpunkte nach Region](/docs/services/key-protect?topic=key-protect-regions#service-endpoints).</dd>

<dt><code>--key-protect-instance GUID_DER_INSTANZ</code></dt>
<dd>Die GUID der {{site.data.keyword.keymanagementserviceshort}}-Instanz. Führen Sie zum Abrufen der Instanz-GUID <code>ibmcloud resource service-instance SERVICEINSTANZNAME --id</code> aus und kopieren Sie den zweiten Wert (nicht den vollständigen Cloudressourcennamen).</dd>

<dt><code>--crk ROOTSCHLÜSSEL-ID</code></dt>
<dd>Die ID des {{site.data.keyword.keymanagementserviceshort}}-Rootschlüssels. Informationen zum Abrufen des CRK finden Sie unter [Schlüssel anzeigen](/docs/services/key-protect?topic=key-protect-view-keys#view-keys).</dd>
</dl>

**Beispiel**:
```
ibmcloud ks key-protect-enable --cluster mycluster --key-protect-url keyprotect.us-south.bluemix.net --key-protect-instance a11aa11a-bbb2-3333-d444-e5e555e5ee5 --crk 1a111a1a-bb22-3c3c-4d44-55e555e55e55
```
{: pre}

</br>
### `ibmcloud ks webhook-create`
{: #cs_webhook_create}

Registriert einen Webhook.
{: shortdesc}



```
ibmcloud ks webhook-create --cluster CLUSTER --level STUFE --type slack --url URL  [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--level <em>STUFE</em></code></dt>
<dd>Die Benachrichtigungsstufe wie etwa <code>Normal</code> oder <code>Warning</code>. <code>Warning</code> ist der Standardwert. Dieser Wert ist optional.</dd>

<dt><code>--type <em>slack</em></code></dt>
<dd>Der Typ des Webhook. Gegenwärtig wird Slack unterstützt. Dieser Wert ist erforderlich.</dd>

<dt><code>--url <em>URL</em></code></dt>
<dd>Die URL für den Webhook. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks webhook-create --cluster mein_cluster --level Normal --type slack --url http://github.com/mywebhook
```
{: pre}

<br />


## Clusterbefehle: Teilnetze
{: #cluster_subnets_commands}



### `ibmcloud ks cluster-subnet-add`
{: #cs_cluster_subnet_add}

Macht ein vorhandenes, portierbares öffentliches oder privates Teilnetz im Konto Ihrer IBM Cloud-Infrastruktur für einen Cluster verfügbar oder verwendet Teilnetze aus einem gelöschten Cluster wieder, anstatt die automatisch bereitgestellten Teilnetze zu verwenden.
{: shortdesc}



<p class="important">Portierbare öffentliche IP-Adressen werden monatlich berechnet. Wenn Sie nach der Bereitstellung Ihres Clusters portierbare öffentliche IP-Adressen entfernen, müssen Sie trotzdem die monatliche Gebühr bezahlen, auch wenn Sie sie nur über einen kurzen Zeitraum genutzt haben.</br>
</br>Wenn Sie ein Teilnetz in einem Cluster verfügbar machen, werden IP-Adressen dieses Teilnetzes zu Zwecken der Clustervernetzung verwendet. Vermeiden Sie IP-Adresskonflikte, indem Sie ein Teilnetz mit nur einem Cluster verwenden. Verwenden Sie kein Teilnetz für mehrere Cluster oder für andere Zwecke außerhalb von {{site.data.keyword.containerlong_notm}} gleichzeitig.</br>
</br>Um die Kommunikation zwischen Workern, die sich in verschiedenen Teilnetzen im selben VLAN in Nicht-VRF-Konten befinden, zu aktivieren, müssen Sie [die Weiterleitung zwischen Teilnetzen im selben VLAN aktivieren](/docs/containers?topic=containers-subnets#subnet-routing).</p>

```
ibmcloud ks cluster-subnet-add --cluster CLUSTER --subnet-id TEILNETZ [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--subnet-id <em>TEILNETZ</em></code></dt>
<dd>Die ID des Teilnetzes. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-subnet-add --cluster mein_cluster --subnet-id 1643389
```
{: pre}

</br>

### `ibmcloud ks cluster-subnet-create`
{: #cs_cluster_subnet_create}

Erstellt ein portierbares Teilnetz in einem Konto der IBM Cloud-Infrastruktur in Ihrem öffentlichen oder private VLAN und macht es für einen Cluster verfügbar.
{: shortdesc}



<p class="important">Wenn Sie ein Teilnetz in einem Cluster verfügbar machen, werden IP-Adressen dieses Teilnetzes zum Zweck von Clusternetzen verwendet. Vermeiden Sie IP-Adresskonflikte, indem Sie ein Teilnetz mit nur einem Cluster verwenden. Verwenden Sie kein Teilnetz für mehrere Cluster oder für andere Zwecke außerhalb von {{site.data.keyword.containerlong_notm}} gleichzeitig.</br>
</br>Wenn Sie über mehrere VLANs für einen Cluster, mehrere Teilnetze in demselben VLAN oder einen Cluster mit mehreren Zonen verfügen, müssen Sie [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) für Ihr Konto der IBM Cloud-Infrastruktur aktivieren, damit die Workerknoten über das private Netz miteinander kommunizieren können. Zur Aktivierung von VRF [wenden Sie sich an den Ansprechpartner für Ihr Konto der IBM Cloud-Infrastruktur](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Wenn Sie prüfen wollen, ob VRF bereits aktiviert wurde, dann verwenden Sie den Befehl `ibmcloud account show`. Wenn Sie VRF nicht aktivieren können oder wollen, aktivieren Sie [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Um diese Aktion durchführen zu können, müssen Sie über [Infrastrukturberechtigung](/docs/containers?topic=containers-users#infra_access) **Netz > VLAN Spanning im Netz verwalten** verfügen oder Sie können den Kontoeigner bitten, diese zu aktivieren. Zum Prüfen, ob VLAN Spanning bereits aktiviert ist, verwenden Sie den [Befehl](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud ks vlan-spanning-get --region <region>`.</p>

```
ibmcloud ks cluster-subnet-create --cluster CLUSTER --size GRÖSSE --vlan VLAN-ID [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich. Zum Auflisten Ihrer Cluster verwenden Sie den [Befehl `ibmcloud ks clusters`](#cs_clusters).</dd>

<dt><code>--size <em>GRÖSSE</em></code></dt>
<dd>Die Anzahl der IP-Adressen, die Sie in dem portierbaren Teilnetz erstellen möchten. Gültige Werte sind 8, 16, 32 oder 64. <p class="note"> Wenn Sie portierbare IP-Adressen für Ihr Teilnetz hinzufügen, werden drei IP-Adressen verwendet, um clusterinterne Netze einzurichten. Diese drei IP-Adressen können nicht für Ihre Ingress-Lastausgleichsfunktionen für Anwendungen (ALBs) oder zum Erstellen von Services für Netzlastausgleichsfunktionen (NLBs) verwendet werden. Wenn Sie beispielsweise acht portierbare öffentliche IP-Adressen anfordern, können Sie fünf verwenden, um die Apps öffentlich verfügbar zu machen.</p> </dd>

<dt><code>--vlan <em>vlan-id</em></code></dt>
<dd>Die ID des öffentlichen oder privaten VLAN, in dem das Teilnetz erstellt werden soll. Sie müssen ein öffentliches oder privates VLAN auswählen, mit dem ein vorhandener Workerknoten verbunden ist. Um die öffentlichen oder privaten VLANs zu prüfen, mit denen Ihre Workerknoten verbunden sind, führen Sie den Befehl <code>ibmcloud ks cluster-get --cluster &lt;cluster&gt; --showResources</code> aus suchen in der Ausgabe nach dem Abschnitt für VLANs von Teilnetzen (<strong>Subnet VLANs</strong>). Das Teilnetz wird in derselben Zone bereitgestellt, in der sich das VLAN befindet.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-subnet-create --cluster mein_cluster --size 8 --vlan 1764905
```
{: pre}

</br>

### `ibmcloud ks cluster-subnet-detach`
{: #cs_cluster_subnet_detach}

Gibt ein portierbares öffentliches oder privates Teilnetz in einem Konto der IBM Cloud-Infrastruktur in einem Cluster frei. Das Teilnetz bleibt in Ihrem Konto in der IBM Cloud-Infrastruktur verfügbar. **Hinweis**: Alle Services, die für eine IP-Adresse aus dem Teilnetz bereitgestellt wurden, bleiben nach der Entfernung des Teilnetzes aktiv.
{: shortdesc}

<p class="note"><img src="images/icon-classic.png" alt="Symbol für Provider der klassischen Infrastruktur" width="15" style="width:15px; border-style: none"/> Befehl nur für klassische Infrastruktur.</p>

```
ibmcloud ks cluster-subnet-detach --cluster CLUSTER --subent-id TEILNETZ-ID [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich. Zum Auflisten Ihrer Cluster verwenden Sie den [Befehl `ibmcloud ks clusters`](#cs_clusters).</dd>

<dt><code>--vlan <em>vlan-id</em></code></dt>
<dd>Die ID des öffentlichen oder privaten Teilnetzes, das freigegeben werden soll. Zum Suchen der Teilnetz-ID müssen Sie zunächst den Befehl <code>ibmcloud ks cluster-get --cluster &lt;cluster&gt; --showResources</code> ausführen und das Teilnetz-CIDR im Abschnitt für <strong>Teilnetz-VLANs</strong> der Ausgabe suchen. Mit dem Teilnetz-CIDR führen Sie dann den Befehl <code>ibmcloud ks subnets</code> aus und suchen nach der <strong>ID</strong> des Teilnetzes.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-subnet-detach --cluster mein_cluster --subnet-id 1602829
```
{: pre}

</br>

### `ibmcloud ks cluster-user-subnet-add`
{: #cs_cluster_user_subnet_add}

Verwenden Sie das eigene private Teilnetz in Ihren {{site.data.keyword.containerlong_notm}}-Clustern.
{: shortdesc}



Dieses private Teilnetz wird nicht von der IBM Cloud-Infrastruktur bereitgestellt. Deshalb müssen Sie das gesamte Routing für ein- und ausgehenden Netzverkehr für das Teilnetz konfigurieren. Um ein Teilnetz der IBM Cloud-Infrastruktur hinzuzufügen, verwenden Sie den [Befehl](#cs_cluster_subnet_add) `ibmcloud ks cluster-subnet-add`.

<p class="important">Wenn Sie ein Teilnetz in einem Cluster verfügbar machen, werden IP-Adressen dieses Teilnetzes zum Zweck von Clusternetzen verwendet. Vermeiden Sie IP-Adresskonflikte, indem Sie ein Teilnetz mit nur einem Cluster verwenden. Verwenden Sie kein Teilnetz für mehrere Cluster oder für andere Zwecke außerhalb von {{site.data.keyword.containerlong_notm}} gleichzeitig.</br>
</br>Wenn Sie über mehrere VLANs für einen Cluster, mehrere Teilnetze in demselben VLAN oder einen Cluster mit mehreren Zonen verfügen, müssen Sie [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) für Ihr Konto der IBM Cloud-Infrastruktur aktivieren, damit die Workerknoten über das private Netz miteinander kommunizieren können. Zur Aktivierung von VRF [wenden Sie sich an den Ansprechpartner für Ihr Konto der IBM Cloud-Infrastruktur](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Wenn Sie prüfen wollen, ob VRF bereits aktiviert wurde, dann verwenden Sie den Befehl `ibmcloud account show`. Wenn Sie VRF nicht aktivieren können oder wollen, aktivieren Sie [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Um diese Aktion durchführen zu können, müssen Sie über [Infrastrukturberechtigung](/docs/containers?topic=containers-users#infra_access) **Netz > VLAN Spanning im Netz verwalten** verfügen oder Sie können den Kontoeigner bitten, diese zu aktivieren. Zum Prüfen, ob VLAN Spanning bereits aktiviert ist, verwenden Sie den [Befehl](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud ks vlan-spanning-get --region <region>`.</p>

```
ibmcloud ks cluster-user-subnet-add --cluster CLUSTER --subnet-cidr TEILNETZ-CIDR --private-vlan PRIVATES_VLAN
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--subnet-cidr <em>TEILNETZ-CIDR</em></code></dt>
<dd>Das CIDR (Classless InterDomain Routing) des Teilnetzes. Dieser Wert ist erforderlich und darf keinen Konflikt mit einem anderen Teilnetz verursachen, das von der IBM Cloud-Infrastruktur verwendet wird. Die unterstützten Präfixe liegen zwischen `/30` (1 IP-Adresse) und `/24` (253 IP-Adressen). Wenn Sie das CIDR mit einer Präfixlänge festlegen und später ändern müssen, dann sollten Sie zuerst das neue CIDR hinzufügen und anschließend das [alte CIDR entfernen](#cs_cluster_user_subnet_rm).</dd>

<dt><code>--private-vlan <em>PRIVATES_VLAN</em></code></dt>
<dd>Die ID des privaten VLAN. Dieser Wert ist erforderlich. Die ID muss einem privaten VLAN in dem Cluster zugeordnet sein, in dem sich mindestens einer der Workerknoten befindet. Um private VLANs in Ihrem Cluster anzeigen zu können, müssen Sie den Befehl `ibmcloud ks cluster-get --cluster <cluster_name_or_ID> --showResources` ausführen. Suchen Sie im Abschnitt für **Teilnetz-VLANs** der Ausgabe nach VLANs, deren Wert für **Public** auf `false` eingestellt ist.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-user-subnet-add --cluster mein_cluster --subnet-cidr 169.xx.xxx.xxx/29 --private-vlan 1502175
```
{: pre}

</br>
### `ibmcloud ks cluster-user-subnet-rm`
{: #cs_cluster_user_subnet_rm}

Entfernt das eigene private Teilnetz aus einem angegebenen Cluster. Jeder Service, der mit einer IP-Adresse aus dem eigenen privaten Teilnetz bereitgestellt wurde, bleibt nach der Entfernung des Teilnetzes weiterhin aktiv.
{: shortdesc}



```
ibmcloud ks cluster-user-subnet-rm --cluster CLUSTER --subnet-cidr TEILNETZ-CIDR --private-vlan PRIVATES_VLAN
```
{: pre}
**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--subnet-cidr <em>TEILNETZ-CIDR</em></code></dt>
<dd>Das CIDR (Classless InterDomain Routing) des Teilnetzes. Dieser Wert ist erforderlich und muss mit dem CIDR übereinstimmen, das mit dem [Befehl `ibmcloud ks cluster-user-subnet-add`](#cs_cluster_user_subnet_add) festgelegt wurde.</dd>

<dt><code>--private-vlan <em>PRIVATES_VLAN</em></code></dt>
<dd>Die ID des privaten VLAN. Dieser Wert ist erforderlich und muss mit der VLAN-ID übereinstimmen, die mit dem [Befehl `bmcloud ks cluster-user-subnet-add`](#cs_cluster_user_subnet_add) festgelegt wurde.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks cluster-user-subnet-rm --cluster mein_cluster --subnet-cidr 169.xx.xxx.xxx/29 --private-vlan 1502175
```
{: pre}

</br>
### `ibmcloud ks subnets`
{: #cs_subnets}

Listet verfügbare portierbare Teilnetze in Ihrem Konto für die IBM Cloud-Infrastruktur auf.
{: shortdesc}



```
ibmcloud ks subnets [--locations STANDORTE] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>

<dt><code>--locations <em>STANDORT</em></code></dt>
<dd>Filtert Zonen nach einem bestimmten Standort oder nach einer Liste durch Kommas getrennter Standorte. Führen Sie den Befehl <code>ibmcloud ks supported-locations</code> aus, um die unterstützten Standorte anzuzeigen.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks subnets --locations ams03,wdc,ap
```
{: pre}

<br />


## Ingress-Befehle für die Lastausgleichsfunktion für Anwendungen (ALB)
{: #alb_commands}

### `ibmcloud ks alb-autoupdate-disable`
{: #cs_alb_autoupdate_disable}

Inaktiviert automatische Aktualisierungen für alle Ingress-ALB-Pods in einem Cluster.
{: shortdesc}



Standardmäßig sind automatische Aktualisierungen für das Ingress-ALB-Add-on (Application Load Balancer, Lastausgleichsfunktion für Anwendungen) aktiviert. ALB-Pods werden automatisch aktualisiert, wenn eine neue Buildversion verfügbar ist. Wenn Sie das Add-on stattdessen manuell aktualisieren möchten, inaktivieren Sie mit diesem Befehl die automatischen Aktualisierungen. Anschließend können Sie ALB-Pods aktualisieren, indem Sie den [Befehl `ibmcloud ks alb-update`](#cs_alb_update) ausführen.

Wenn Sie die Kubernetes-Hauptversion oder -Nebenversion Ihres Clusters aktualisieren, nimmt IBM automatisch die erforderlichen Änderungen an der Ingress-Bereitstellung vor, ändert aber nicht die Buildversion Ihres Add-ons für die Lastausgleichsfunktion für Ihre Ingress-Anwendungen. Sie sind dafür verantwortlich, die Kompatibilität der aktuellen Kubernetes-Versionen und Ihrer Images des Add-ons für die Ingress-Lastausgleichsfunktion für Anwendungen (ALB) zu prüfen.

```
ibmcloud ks alb-autoupdate-disable --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Beispiel**:
```
ibmcloud ks alb-autoupdate-disable --cluster mycluster
```
{: pre}

</br>
### `ibmcloud ks alb-autoupdate-enable`
{: #cs_alb_autoupdate_enable}

Aktiviert automatische Aktualisierungen für alle Ingress-ALB-Pods in einem Cluster.
{: shortdesc}

Wenn die automatischen Aktualisierungen für das Ingress-ALB-Add-on inaktiviert sind, können Sie diese wieder aktivieren. Sobald die nächste Buildversion verfügbar ist, werden die ALBs automatisch auf den neuen Build aktualisiert.



```
ibmcloud ks alb-autoupdate-enable --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud ks alb-autoupdate-get`
{: #cs_alb_autoupdate_get}

Prüft, ob die automatischen Aktualisierungen für das Ingress-ALB-Add-on aktiviert sind und ob Ihre ALBs auf die neueste Buildversion aktualisiert wurden.
{: shortdesc}



```
ibmcloud ks alb-autoupdate-get --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

</br>
### Betaversion: `ibmcloud ks alb-cert-deploy`
{: #cs_alb_cert_deploy}

Stellt für die Lastausgleichsfunktion für Anwendungen (ALB) in einem Cluster ein Zertifikat bereit oder aktualisiert ein Zertifikat aus der verwendeten Instanz von {{site.data.keyword.cloudcerts_long_notm}}.
{: shortdesc}



Wenn Sie ein Zertifikat mit diesem Befehl importieren, wird der geheime Schlüssel für das Zertifikat in einem Namensbereich mit dem Namen `ibm-cert-store` erstellt. Anschließend wird ein Verweis auf diesen geheimen Schlüssel im Namensbereich `default` erstellt, auf den jede Ingress-Ressource in einem beliebigen Namensbereich zugreifen kann. Wenn die ALB Anforderungen verarbeitet, folgt sie diesem Verweis, um den geheimen Schlüssel für das Zertifikat aus dem Namensbereich `ibm-cert-store` abzurufen und zu verwenden.

Mit dem Parameter `--update` können Sie auch Zertifikate aktualisieren, um z. B. ein Zertifikat in Ihrem Cluster nach der Verlängerung des Zertifikats in {{site.data.keyword.cloudcerts_short}} zu aktualisieren. Sie können ausschließlich Zertifikate aktualisieren, die aus derselben Instanz von {{site.data.keyword.cloudcerts_long_notm}} importiert wurden.


Zur Einhaltung der [Ratengrenzwerte](https://cloud.ibm.com/apidocs/certificate-manager#rate-limiting), die von {{site.data.keyword.cloudcerts_short}} festgelegt werden, warten Sie mindestens 45 Sekunden zwischen aufeinander folgenden Befehlen `alb-cert-deploy` und `alb-cert-deploy --update` ab.
{: note}

```
ibmcloud ks alb-cert-deploy [--update] --cluster CLUSTER --secret-name NAME_DES_GEHEIMEN_SCHLÜSSELS --cert-crn CRN_DES_ZERTIFIKATS [--update] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--update</code></dt>
<dd>Aktualisieren Sie das Zertifikat für einen geheimen Schlüssel der Lastausgleichsfunktion für Anwendungen (ALB) in einem Cluster. Sie können diesen Parameter verwenden, um das Zertifikat zu aktualisieren, nachdem Sie es in {{site.data.keyword.cloudcerts_short}} verlängert haben.</dd>

<dt><code>--secret-name <em>NAME_DES_GEHEIMEN_SCHLÜSSELS</em></code></dt>
<dd>Geben Sie einen Namen für den geheimen ALB-Schlüssel an, wenn er im Cluster erstellt wird. Dieser Wert ist erforderlich. Stellen Sie sicher, dass Sie den geheimen Schlüssel mit einem Namen erstellen, der sich vom Namen des von IBM bereitgestellten geheimen Ingress-Schlüssels unterscheidet. Sie können den Namen des von IBM bereitgestellten geheimen Ingress-Schlüssels mit dem Befehl <code>ibmcloud ks cluster-get --cluster <clustername_oder_-id> | grep Ingress</code> abrufen.</dd>

<dt><code>--cert-crn <em>CRN_DES_ZERTIFIKATS</em></code></dt>
<dd>Die CRN des Zertifikats. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiele**:

Beispiel für die Bereitstellung eines geheimen ALB-Schlüssels:
```
ibmcloud ks alb-cert-deploy --secret-name mein_geheimer_schlüssel_der_alb --cluster mein_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

Beispiel für die Aktualisierung eines vorhandenen geheimen ALB-Schlüssels:
```
ibmcloud ks alb-cert-deploy --update --secret-name mein_geheimer_schlüssel_der_alb --cluster mein_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:7e21fde8ee84a96d29240327daee3eb2
```
{: pre}

</br>
### Betaversion: `ibmcloud ks alb-cert-get`
{: #cs_alb_cert_get}

Wenn Sie ein Zertifikat aus {{site.data.keyword.cloudcerts_short}} in die ALB in einem Cluster importiert haben, können Sie mit diesem Befehl Informationen zum TLS-Zertifikat anzeigen, wie zum Beispiel die geheimen Schlüssel, die dem Zertifikat zugeordnet sind.
{: shortdesc}



```
ibmcloud ks alb-cert-get --cluster CLUSTER [--secret-name NAME_DES_GEHEIMEN_SCHLÜSSELS] [--cert-crn CRN_DES_ZERTIFIKATS] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--secret-name <em>NAME_DES_GEHEIMEN_SCHLÜSSELS</em></code></dt>
<dd>Der Name des geheimen Schlüssels der Lastausgleichsfunktion für Anwendungen (Application Load Balancer, ALB). Dieser Wert ist erforderlich, um Informationen zu einem bestimmten geheimen ALB-Schlüssel im Cluster abzurufen.</dd>

<dt><code>--cert-crn <em>CRN_DES_ZERTIFIKATS</em></code></dt>
<dd>Die CRN des Zertifikats. Dieser Wert ist erforderlich, um Informationen zu allen geheimen ALB-Schlüsseln abzurufen, die mit dem CRN eines bestimmten Zertifikats im Cluster übereinstimmen.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiele**:

Beispiel für das Abrufen von Informationen zu einem geheimen ALB-Schlüssel:
```
ibmcloud ks alb-cert-get --cluster mein_cluster --secret-name mein_geheimer_schlüssel_der_alb
```
{: pre}

Beispiel für das Abrufen von Informationen zu allen geheimen ALB-Schlüsseln, die mit der CRN eines bestimmten Zertifikats übereinstimmen:
```
ibmcloud ks alb-cert-get --cluster mein_cluster --cert-crn  crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

</br>
### Betaversion: `ibmcloud ks alb-cert-rm`
{: #cs_alb_cert_rm}

Wenn Sie ein Zertifikat aus {{site.data.keyword.cloudcerts_short}} in die ALB in einem Cluster importiert haben, können Sie den geheimen Schlüssel mit diesem Befehl aus dem Cluster entfernen.
{: shortdesc}



Zur Einhaltung der [Ratengrenzwerte](https://cloud.ibm.com/apidocs/certificate-manager#rate-limiting), die von {{site.data.keyword.cloudcerts_short}} festgelegt werden, warten Sie mindestens 45 Sekunden zwischen aufeinander folgenden Befehlen `alb-cert-rm` ab.
{: note}

```
ibmcloud ks alb-cert-rm --cluster CLUSTER [--secret-name NAME_DES_GEHEIMEN_SCHLÜSSELS] [--cert-crn CRN_DES_ZERTIFIKATS] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--secret-name <em>NAME_DES_GEHEIMEN_SCHLÜSSELS</em></code></dt>
<dd>Der Name des geheimen Schlüssels der Lastausgleichsfunktion für Anwendungen (Application Load Balancer, ALB). Dieser Wert ist erforderlich, um einen bestimmten geheimen ALB-Schlüssel im Cluster zu entfernen.</dd>

<dt><code>--cert-crn <em>CRN_DES_ZERTIFIKATS</em></code></dt>
<dd>Der CRN des Zertifikats. Dieser Wert ist erforderlich, um alle geheimen ALB-Schlüssel zu entfernen, die mit dem CRN eines bestimmten Zertifikats im Cluster übereinstimmen.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>

</dl>

**Beispiele**:

Beispiel für das Entfernen eines geheimen ALB-Schlüssels:
```
ibmcloud ks alb-cert-rm --cluster mein_cluster --secret-name mein_geheimer_schlüssel_der_alb
```
{: pre}

Beispiel für das Entfernen aller geheimen ALB-Schlüssel, die mit der CRN eines bestimmten Zertifikats übereinstimmen:
```
ibmcloud ks alb-cert-rm --cluster mein_cluster --cert-crn crn:v1:staging:public:cloudcerts:us-south:a/06580c923e40314421d3b6cb40c01c68:0db4351b-0ee1-479d-af37-56a4da9ef30f:certificate:4bc35b7e0badb304e60aef00947ae7ff
```
{: pre}

</br>
### `ibmcloud ks alb-certs`
{: #cs_alb_certs}

Listet die Zertifikate auf, die Sie aus Ihrer {{site.data.keyword.cloudcerts_long_notm}}-Instanz in ALBs in einem Cluster importiert haben.
{: shortdesc}



```
ibmcloud ks alb-certs --cluster CLUSTER [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**

<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks alb-certs --cluster mein_cluster
```
{: pre}

</br>
### `ibmcloud ks alb-configure`
{: #cs_alb_configure}

Aktiviert oder inaktiviert eine Lastausgleichsfunktion für Anwendungen (ALB) in Ihrem Standardcluster.
{: shortdesc}

Sie können diesen Befehl für Folgendes verwenden:
* Aktivieren Sie eine private Standard-ALB. Wenn Sie einen Cluster erstellen, wird für Sie in jeder Zone, in der sich Worker und ein verfügbares privates Teilnetz befinden, eine private Standard-ALB erstellt, aber die privaten Standard-ALBs sind nicht aktiviert. Allerdings werden alle standardmäßigen öffentlichen ALBs automatisch aktiviert.
* Aktivieren Sie eine ALB, die Sie zuvor inaktiviert haben.
* Inaktivieren Sie eine ALB.
* Inaktivieren Sie die von IBM bereitgestellte ALB-Bereitstellung, sodass Sie Ihren eigenen Ingress-Controller bereitstellen und die DNS-Registrierung für die von IBM bereitgestellte Ingress-Unterdomäne oder den Lastausgleichsservice nutzen können, der zum Bereitstellen des Ingress-Controllers verwendet wird.

```
ibmcloud ks alb-configure --albID ALB-ID --disable|--enable [--user-ip BENUTZER-IP]|--disable-deployment [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--albID <em>ALB-ID</em></code></dt>
<dd>Die ID für eine ALB. Zum Anzeigen der IDs für die ALBs in einem Cluster führen Sie den Befehl <code>ibmcloud ks albs --cluster <em>CLUSTER</em></code> aus. Dieser Wert ist erforderlich.</dd>

<dt><code>--disable</code></dt>
<dd>Schließen Sie dieses Flag ein, um eine ALB in einem Cluster zu inaktivieren. <p class="note">Wenn Sie eine ALB inaktivieren, wird die IP-Adresse, die die ALB verwendet hat, wieder in den Pool der verfügbaren portierbaren IPs zurückgestellt, sodass ein anderer Service die IP verwenden kann. Wenn Sie später versuchen, die ALB erneut zu aktivieren, meldet die ALB möglicherweise einen Fehler, wenn die bisher von ihr verwendete IP-Adresse jetzt von einem anderen Service verwendet wird. Sie können entweder die Ausführung des anderen Service stoppen oder eine andere IP-Adresse angeben, die verwendet werden soll, wenn Sie die ALB erneut aktivieren.</p></dd>

<dt><code>--enable</code></dt>
<dd>Schließen Sie dieses Flag ein, um eine ALB in einem Cluster zu aktivieren.</dd>

<dt><code>--user-ip <em>BENUTZER-IP</em></code></dt>
<dd>Optional: Wenn Sie die ALB mit dem Flag <code>--enable</code> aktivieren, können Sie eine IP-Adresse angeben, die sich in einem VLAN in der Zone befindet, in der die ALB erstellt wurde. Die ALB wird mit dieser öffentlichen oder privaten IP-Adresse aktiviert und verwendet diese Adresse. <strong>Hinweis</strong>: Diese IP-Adresse darf weder von einer anderen Lastausgleichsfunktion noch von einer anderen ALB im Cluster verwendet werden. Wird keine IP-Adresse bereitgestellt, wird die ALB mit einer öffentlichen oder privaten IP-Adresse aus dem portierbaren, öffentlichen oder privaten Teilnetz, die beim Erstellen des Clusters automatisch bereitgestellt wurde, oder mit der öffentlichen oder privaten IP-Adresse bereitgestellt, die Sie der ALB zuvor zugeordnet haben.</dd>

<dt><code>--disable-deployment</code></dt>
<dd>Schließen Sie dieses Flag ein, um die von IBM bereitgestellte ALB-Bereitstellung zu inaktivieren. Bei Verwendung dieses Flags wird nicht die DNS-Registrierung für die von IBM bereitgestellte Ingress-Unterdomäne oder der Lastausgleichsservice, der zum Bereitstellen des Ingress-Controllers verwendet wird, entfernt.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiele**:

Beispiel für die Aktivierung einer ALB:
```
ibmcloud ks alb-configure --albID private-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --enable
```
{: pre}

Beispiel für die Aktivierung einer ALB mit einer von einem Benutzer bereitgestellten IP-Adresse:
```
ibmcloud ks alb-configure --albID private-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --enable --user-ip benutzer-ip
```
{: pre}

Beispiel für die Inaktivierung einer ALB:
```
ibmcloud ks alb-configure --albID public-cr18a61a63a6a94b658596aa93a087aaa9-alb1 --disable
```
{: pre}

</br>

### `ibmcloud ks alb-get`
{: #cs_alb_get}

Zeigt die Details einer Ingress-ALB in einem Cluster an.
{: shortdesc}



```
ibmcloud ks alb-get --albID ALB-ID [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--albID <em>ALB-ID</em></code></dt>
<dd>Die ID für eine ALB. Zum Anzeigen der IDs für die ALBs in einem Cluster führen Sie den Befehl <code>ibmcloud ks albs --cluster <em>CLUSTER</em></code> aus. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks alb-get --albID public-cr18a61a63a6a94b658596aa93a087aaa9-alb1
```
{: pre}

</br>
### `ibmcloud ks alb-rollback`
{: #cs_alb_rollback}

Wenn Ihre ALB-Pods vor Kurzem aktualisiert wurden, aber eine angepasste Konfiguration für Ihre ALBs von dem letzten Build betroffen ist, können Sie die Aktualisierung rückgängig machen und auf den Build zurücksetzen, den Ihre ALB-Pods zuvor ausgeführt hatten. Alle ALB-Pods in Ihrem Cluster werden auf ihren vorherigen Laufstatus zurückgesetzt.
{: shortdesc}

Nachdem Sie eine Aktualisierung rückgängig gemacht haben, werden die automatischen Aktualisierungen für ALB-Pods inaktiviert. Um die automatischen Aktualisierungen wieder zu aktivieren, verwenden Sie den [Befehl `alb-autoupdate-enable`](#cs_alb_autoupdate_enable).



```
ibmcloud ks alb-rollback --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud ks alb-types`
{: #cs_alb_types}

Listet die Ingress-ALB-Typen auf, die unterstützt werden.
{: shortdesc}



```
ibmcloud ks alb-types [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

</br>

### `ibmcloud ks alb-update`
{: #cs_alb_update}

Erzwingt eine Aktualisierung der Ingress-ALB-Pods im Cluster auf die neueste Version.
{: shortdesc}



Wenn die automatischen Aktualisierungen für das Ingress-ALB-Add-on inaktiviert sind und Sie das Add-on aktualisieren möchten, können Sie eine einmalige Aktualisierung Ihrer ALB-Pods erzwingen. Wenn Sie das Add-on manuell aktualisieren, werden alle ALB-Pods in dem Cluster auf den neuen Build aktualisiert. Sie können nicht eine einzelne ALB aktualisieren oder auswählen, auf welchen Build das Add-on aktualisiert werden soll. Die automatischen Aktualisierungen bleiben inaktiviert.

Wenn Sie die Kubernetes-Hauptversion oder -Nebenversion Ihres Clusters aktualisieren, nimmt IBM automatisch die erforderlichen Änderungen an der Ingress-Bereitstellung vor, ändert aber nicht die Buildversion Ihres Add-ons für die Lastausgleichsfunktion für Ihre Ingress-Anwendungen. Sie sind dafür verantwortlich, die Kompatibilität der aktuellen Kubernetes-Versionen und Ihrer Images des Add-ons für die Ingress-Lastausgleichsfunktion für Anwendungen (ALB) zu prüfen.

```
ibmcloud ks alb-update --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

</br>
### `ibmcloud ks albs`
{: #cs_albs}

Listet alle Ingress-ALB-IDs in einem Cluster auf und zeigt, ob eine Aktualisierung für die ALB-Pods verfügbar ist.
{: shortdesc}



Wenn keine ALB-IDs zurückgegeben werden, verfügt der Cluster nicht über ein portierbares Teilnetz. Sie können Teilnetze [erstellen](#cs_cluster_subnet_create) oder zu einem Cluster [hinzufügen](#cs_cluster_subnet_add).
{: tip}

```
ibmcloud ks albs --cluster CLUSTER [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code><em>--cluster </em>CLUSTER</code></dt>
<dd>Der Name oder die ID des Clusters, in dem Sie verfügbare Lastausgleichsfunktionen für Anwendungen (ALBs) auflisten. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks albs --cluster mein_cluster
```
{: pre}

<br />



## Befehle für die Infrastruktur
{: #infrastructure_commands}

### `ibmcloud ks api-key-info`
{: #cs_api_key_info}

Zeigt den Namen und die E-Mail-Adresse für den Eigner des {{site.data.keyword.cloud_notm}} IAM-API-Schlüssels (Identity and Access Management) in einer {{site.data.keyword.containerlong_notm}}-Ressourcengruppe an.
{: shortdesc}



Der {{site.data.keyword.cloud_notm}}-API-Schlüssel wird automatisch für eine Ressourcengruppe und Region festgelegt, wenn die erste Aktion ausgeführt wird, für die die {{site.data.keyword.containerlong_notm}}-Administratorzugriffsrichtlinie ausgeführt werden muss. Zum Beispiel erstellt einer Ihrer Benutzer mit Administratorberechtigung den ersten Cluster in der Ressourcengruppe `default` in der Region `us-south`. Dadurch wird der {{site.data.keyword.cloud_notm}} IAM-API-Schlüssel für diesen Benutzer in dem Konto für diese Ressourcengruppe und diese Region gespeichert. Der API-Schlüssel wird verwendet, um Ressourcen in der IBM Cloud-Infrastruktur zu bestellen, z. B. neue Workerknoten oder VLANs. Für jede Region in einer Ressourcengruppe kann ein anderer API-Schlüssel festgelegt werden.

Wenn ein anderer Benutzer eine Aktion in dieser Ressourcengruppe und Region ausführt, die eine Interaktion mit dem Portfolio der IBM Cloud-Infrastruktur erfordert, z. B. die Erstellung eines neuen Clusters oder das erneute Laden eines Workerknotens, wird der gespeicherte API-Schlüssel verwendet, um festzustellen, ob ausreichende Berechtigungen vorhanden sind, um diese Aktion auszuführen. Um sicherzustellen, dass infrastrukturbezogene Aktionen in Ihrem Cluster erfolgreich ausgeführt werden können, weisen Sie Ihre {{site.data.keyword.containerlong_notm}}-Benutzer mit Administratorberechtigung der Infrastrukturzugriffsrichtlinie **Superuser** zu. Weitere Informationen finden unter [Benutzerzugriff verwalten](/docs/containers?topic=containers-users#infra_access).

Wenn Sie feststellen, dass Sie den API-Schlüssel aktualisieren müssen, der für eine Ressourcengruppe und Region gespeichert ist, können Sie dies tun, indem Sie den Befehl [ibmcloud ks api-key-reset](#cs_api_key_reset) ausführen. Dieser Befehl erfordert die {{site.data.keyword.containerlong_notm}}-Administratorzugriffsrichtlinie und speichert den API-Schlüssel des Benutzers, der diesen Befehl ausführt, im Konto.

**Tipp:** Der API-Schlüssel, der in diesem Befehl zurückgegeben wird, wird möglicherweise nicht verwendet, wenn die Berechtigungsnachweise der IBM Cloud-Infrastruktur manuell mithilfe des Befehls [ibmcloud ks credential-set](#cs_credentials_set) festgelegt wurden.

```
ibmcloud ks api-key-info --cluster CLUSTER [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>

</dl>

**Beispiel**:
```
ibmcloud ks api-key-info --cluster mein_cluster
```
{: pre}

</br>
### `ibmcloud ks api-key-reset`
{: #cs_api_key_reset}

Ersetzt den aktuellen {{site.data.keyword.cloud_notm}} IAM-API-Schlüssel in einer {{site.data.keyword.cloud_notm}}-Ressourcengruppe und {{site.data.keyword.containershort_notm}}-Region.
{: shortdesc}



Dieser Befehl erfordert die {{site.data.keyword.containerlong_notm}}-Administratorzugriffsrichtlinie und speichert den API-Schlüssel des Benutzers, der diesen Befehl ausführt, im Konto. Der {{site.data.keyword.cloud_notm}} IAM-API-Schlüssel ist erforderlich, um Infrastruktur aus dem Portfolio der IBM Cloud-Infrastruktur zu bestellen. Einmal gespeichert, wird der API-Schlüssel unabhängig vom Benutzer, der diesen Befehl ausführt, für jede Aktion in einer Region verwendet, die Infrastrukturberechtigungen erfordert. Weitere Informationen zur Funktionsweise von {{site.data.keyword.cloud_notm}} IAM-API-Schlüsseln finden Sie im Abschnitt zum [Befehl `ibmcloud ks api-key-info`](#cs_api_key_info).

Stellen Sie vor Verwendung dieses Befehls sicher, dass der Benutzer, der diesen Befehl ausführt, über die erforderlichen Berechtigungen für [{{site.data.keyword.containerlong_notm}} und die IBM Cloud-Infrastruktur verfügt.](/docs/containers?topic=containers-users#users). Geben Sie die Ressourcengruppe und die Region als Ziel an, für die Sie den API-Schlüssel festlegen möchten.
{: important}

```
ibmcloud ks api-key-reset --region REGION [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Geben Sie eine Region an. Führen Sie den Befehl <code>ibmcloud ks regions</code> aus, um die verfügbaren Regionen aufzuführen.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks api-key-reset --region us-south
```
{: pre}


</br>

### `ibmcloud ks credential-get`
{: #cs_credential_get}

Wenn Sie Ihr {{site.data.keyword.cloud_notm}}-Konto so konfigurieren, dass für den Zugriff auf das Portfolio der IBM Cloud-Infrastruktur unterschiedliche Berechtigungsnachweise verwendet werden, können Sie mit diesem Befehl den Namen des Infrastrukturbenutzers für die Region und die Ressourcengruppe abrufen, die Sie zurzeit als Ziel angegeben haben.
{: shortdesc}



```
ibmcloud ks credential-get --region REGION [-s] [--json]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Geben Sie eine Region an. Führen Sie den Befehl <code>ibmcloud ks regions</code> aus, um die verfügbaren Regionen aufzuführen.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks credential-get --region us-south
```
{: pre}

</br>
### `ibmcloud ks credential-set` (`credentials-set`)
{: #cs_credentials_set}

Legt Berechtigungsnachweise für eine Ressourcengruppe und Region fest, mit denen Sie über Ihr {{site.data.keyword.cloud_notm}}-Konto auf das Portfolio der IBM Cloud-Infrastruktur zugreifen können.
{: shortdesc}



Wenn Sie über ein nutzungsabhängiges {{site.data.keyword.cloud_notm}}-Konto verfügen, haben Sie standardmäßig Zugriff auf ein verknüpftes Portfolio der IBM Cloud-Infrastruktur. Es kann jedoch sein, dass Sie ein anderes Konto der IBM Cloud-Infrastruktur verwenden möchten, das Sie bereits für die Infrastrukturbestellung verwenden. Sie können dieses Infrastrukturkonto über den folgenden Befehl mit Ihrem {{site.data.keyword.cloud_notm}}-Konto verknüpfen.

Falls die Berechtigungsnachweise für die IBM Cloud-Infrastruktur für eine Region und Ressourcengruppe manuell definiert wurden, werden diese Berechtigungsnachweise für die Bestellung von Infrastruktur für alle Cluster innerhalb der Region in der Ressourcengruppe verwendet. Diese Berechtigungsnachweise werden verwendet, um Infrastrukturberechtigungen zu bestimmen, selbst wenn bereits ein [{{site.data.keyword.cloud_notm}} IAM-API-Schlüssel](#cs_api_key_info) für die Ressourcengruppe und Region vorhanden ist. Wenn der Benutzer, dessen Berechtigungsnachweise gespeichert wurden, nicht über die erforderlichen Berechtigungen zum Bestellen von Infrastruktur verfügt, können infrastrukturbezogene Aktionen, wie z. B. das Erstellen eines Clusters oder das erneute Laden eines Workerknotens, fehlschlagen.

Sie können nicht mehrere Berechtigungsnachweise für dieselbe {{site.data.keyword.containerlong_notm}}-Ressourcengruppe und -Region festlegen.

Stellen Sie vor Verwendung dieses Befehls sicher, dass der Benutzer, dessen Berechtigungsnachweise verwendet werden, über die erforderlichen Berechtigungen für [{{site.data.keyword.containerlong_notm}} und die IBM Cloud-Infrastruktur verfügt](/docs/containers?topic=containers-users#users).
{: important}

```
ibmcloud ks credential-set --infrastructure-api-key API-SCHLÜSSEL --infrastructure-username BENUTZERNAME --region REGION [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--infrastructure-username <em>BENUTZERNAME</em></code></dt>
<dd>Der API-Benutzername für ein Konto der IBM Cloud-Infrastruktur. Dieser Wert ist erforderlich. Der API-Benutzername für die Infrastruktur ist nicht mit der IBMid identisch. Informationen zum Anzeigen des API-Benutzernamens für die Infrastruktur finden Sie unter [API-Schlüssel für klassische Infrastruktur verwalten](/docs/iam?topic=iam-classic_keys).</dd>

<dt><code>--infrastructure-api-key <em>API-SCHLÜSSEL</em></code></dt>
<dd>Der API-Schlüssel für ein Konto der IBM Cloud-Infrastruktur. Dieser Wert ist erforderlich. Informationen zum Anzeigen oder Generieren eines Infrastruktur-API-Schlüssels finden Sie unter [API-Schlüssel für klassische Infrastruktur verwalten](/docs/iam?topic=iam-classic_keys).</dd>

<dt><code>--region <em>REGION</em></code></dt>
<dd>Geben Sie eine Region an. Führen Sie den Befehl <code>ibmcloud ks regions</code> aus, um die verfügbaren Regionen aufzuführen.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks credential-set --infrastructure-api-key <api-schlüssel> --infrastructure-username dbmanager --region us-south
```
{: pre}

</br>
### `ibmcloud ks credential-unset`
{: #cs_credentials_unset}

Entfernt die Berechtigungsnachweise für eine Ressourcengruppe und Region, um den Zugriff auf das Portfolio der IBM Cloud-Infrastruktur über Ihr {{site.data.keyword.cloud_notm}}-Konto zu entfernen.
{: shortdesc}

Nachdem Sie die Berechtigungsnachweise entfernt haben, wird der [{{site.data.keyword.cloud_notm}} IAM-API-Schlüssel](#cs_api_key_info) verwendet, um Ressourcen in der IBM Cloud-Infrastruktur zu bestellen.



```
ibmcloud ks credential-unset --region REGION [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Geben Sie eine Region an. Führen Sie den Befehl <code>ibmcloud ks regions</code> aus, um die verfügbaren Regionen aufzuführen.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks credential-unset --region us-south
```
{: pre}

</br>

### `ibmcloud ks flavors` (`machine-types`)
{: #cs_machine_types}

Zeigt eine Liste der verfügbaren Workerknotentypen an. Die Typen können abhängig von der jeweiligen Zone variieren.
{:shortdesc}



Jeder Typ enthält die Menge an virtueller CPU, Speicher und Plattenspeicher für jeden Workerknoten im Cluster. Das sekundäre Speicherplattenverzeichnis, in dem alle Containerdaten gespeichert sind, wird standardmäßig mit der LUKS-Verschlüsselung verschlüsselt. Wenn die Option `disable-disk-encrypt` während der Clustererstellung eingeschlossen wird, werden die Containerlaufzeitdaten des Hosts nicht verschlüsselt. [Weitere Informationen zur Verschlüsselung](/docs/containers?topic=containers-security#encrypted_disk).

Sie können Ihren Workerknoten als virtuelle Maschine auf gemeinsam genutzter oder dedizierter Hardware bereitstellen oder (nur für klassische Cluster) als physische Maschine auf Bare-Metal-Systemen. [Erfahren Sie mehr über die Optionen für Typen](/docs/containers?topic=containers-planning_worker_nodes#planning_worker_nodes).

```
ibmcloud ks flavors --zone ZONE [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Geben Sie die Zone ein, in der die verfügbaren Typen aufgelistet werden sollen. Dieser Wert ist erforderlich. Um die verfügbaren Zonen für klassische Cluster anzuzeigen, führen Sie den Befehl `ibmcloud ks zones` aus.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks flavors --zone dal10
```
{: pre}


</br>

### `ibmcloud ks infra-permissions-get`
{: #infra_permissions_get}

Prüft, ob in den Berechtigungsnachweisen für den [Zugriff auf das Portfolio der IBM Cloud-Infrastruktur](/docs/containers?topic=containers-users#api_key) für die Zielressourcengruppe und -region vorgeschlagene oder erforderliche Infrastrukturberechtigungen fehlen.
{: shortdesc}



**Was sind `erforderliche` und `vorgeschlagene` Infrastrukturberechtigungen?**<br>
Wenn den Infrastrukturberechtigungsnachweisen für die Region und die Ressourcengruppe Berechtigungen fehlen, gibt die Ausgabe dieses Befehls eine Liste der `erforderlichen` (Required) und `vorgeschlagenen` (Suggested) Berechtigungen zurück.
*   **Erforderlich**: Diese Berechtigungen sind erforderlich, um Infrastrukturressourcen, wie z. B. Workerknoten, erfolgreich zu bestellen und zu verwalten. Wenn für die Infrastrukturberechtigungsnachweise eine dieser Berechtigungen fehlt, können gängige Aktionen wie `worker-reload` für alle Cluster in der Region und der Ressourcengruppe fehlschlagen.
*   **Vorgeschlagen**: Es ist hilfreich, diese Berechtigungen in Ihre Infrastrukturberechtigungen einzuschließen. In bestimmten Fällen können sie erforderlich sein. Beispielsweise wird die Infrastrukturberechtigung `Datenverarbeitungsservice mit Port für öffentliches Netz hinzufügen` vorgeschlagen, da Sie diese Berechtigung für einen öffentlichen Netzbetrieb benötigen. Wenn Sie allerdings nur mit einem Cluster im privaten VLAN arbeiten, wird die Berechtigung nicht benötigt und wird daher nicht als `erforderlich` betrachtet.

Eine Liste gängiger Anwendungsfälle, sortiert nach Berechtigung, finden Sie unter [Infrastrukturrollen](/docs/containers?topic=containers-access_reference#infra).

**Was ist, wenn ich eine Infrastrukturberechtigung sehe, die ich in der Konsole oder in der Tabelle mit den [Infrastrukturrollen](/docs/containers?topic=containers-access_reference#infra) nicht finden kann?**<br>
`Supportfallberechtigungen` werden in einem anderen Teil der Konsole verarbeitet als Infrastrukturberechtigungen. Weitere Informationen finden Sie in Schritt 8 unter [Infrastrukturberechtigungen anpassen](/docs/containers?topic=containers-users#infra_access).

**Welche Infrastrukturberechtigungen ordne ich zu?**<br>
Wenn die Richtlinien Ihres Unternehmens für Berechtigungen streng sind, müssen Sie möglicherweise die `vorgeschlagenen` Berechtigungen für den Anwendungsfall Ihres Clusters begrenzen. Andernfalls müssen Sie sicherstellen, dass Ihre Infrastrukturberechtigungsnachweise für die Region und die Ressourcengruppe alle `erforderlichen` und `vorgeschlagenen` Berechtigungen enthalten.

In den meisten Anwendungsfällen [richten Sie den API-Schlüssel](/docs/containers?topic=containers-users#api_key) für die Region und die Ressourcengruppe mit den entsprechenden Infrastrukturberechtigungen ein. Wenn Sie ein anderes Infrastrukturkonto als Ihr aktuelles Konto verwenden müssen, [konfigurieren Sie die Berechtigungsnachweise manuell](/docs/containers?topic=containers-users#credentials).

**Wie kann ich steuern, welche Aktionen die Benutzer ausführen können?**<br>
Nachdem die Infrastrukturberechtigungsnachweise eingerichtet wurden, können Sie steuern, welche Aktionen Ihre Benutzer ausführen können, indem Sie ihnen [{{site.data.keyword.cloud_notm}} IAM-Plattformrollen](/docs/containers?topic=containers-access_reference#iam_platform) zuordnen.

```
ibmcloud ks infra-permissions-get --region REGION [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Geben Sie eine Region an. Führen Sie den Befehl <code>ibmcloud ks regions</code> aus, um die verfügbaren Regionen aufzuführen. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks infra-permissions-get --region us-south
```
{: pre}

Beispielausgabe:
```
Missing Virtual Worker Permissions

Add Server                    suggested
Cancel Server                 suggested
View Virtual Server Details   required

Missing Physical Worker Permissions

No changes are suggested or required.

Missing Network Permissions

No changes are suggested or required.

Missing Storage Permissions

Add Storage       required
Manage Storage    required
```
{: screen}


</br>

### `ibmcloud ks vlan-spanning-get`
{: #cs_vlan_spanning_get}

Zeigt den VLAN Spanning-Status für ein Konto der IBM Cloud-Infrastruktur an. Über VLAN Spanning können alle Einheiten eines Kontos über das private Netz miteinander kommunizieren, und zwar unabhängig vom zugeordneten VLAN.
{: shortdesc}

<p class="note">Die Option für VLAN Spanning wird für Cluster inaktiviert, die in einem VRF-fähigen Konto erstellt werden. Wenn VRF aktiviert ist, können alle VLANs im Konto automatisch über das private Netz miteinander kommunizieren. Wenn Sie prüfen wollen, ob VRF aktiviert wurde, dann verwenden Sie den Befehl `ibmcloud account show`. Weitere Informationen finden Sie unter [Konfiguration des Clusternetzes planen: Kommunikation zwischen Workern](/docs/containers?topic=containers-plan_clusters#worker-worker).
</p>

```
ibmcloud ks vlan-spanning-get --region REGION [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Geben Sie eine Region an. Führen Sie den Befehl <code>ibmcloud ks regions</code> aus, um die verfügbaren Regionen aufzuführen.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks vlan-spanning-get --region us-south
```
{: pre}

</br>
### `ibmcloud ks vlans`
{: #cs_vlans}

Listet die öffentlichen und privaten VLANs auf, die in einer Zone in Ihrem Konto der IBM Cloud-Infrastruktur zur Verfügung stehen. Um verfügbare VLANs auflisten zu können, müssen Sie über ein gebührenpflichtiges Konto verfügen.
{: shortdesc}



```
ibmcloud ks vlans --zone ZONE [--all] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:**
* Anzeigen der VLANs, mit denen der Cluster in einer Zone verbunden ist: Plattformrolle **Anzeigeberechtigter** für den Cluster in {{site.data.keyword.containerlong_notm}}
* Auflisten aller verfügbaren VLANs in einer Zone: Plattformrolle **Anzeigeberechtigter** für die Region in {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Geben Sie die Zone ein, in der Sie Ihre privaten und öffentlichen VLANs auflisten möchten. Dieser Wert ist erforderlich. Um die verfügbaren Zonen anzuzeigen, führen Sie den Befehl `ibmcloud ks zones` aus.</dd>

<dt><code>--all</code></dt>
<dd>Listet alle verfügbaren VLANs auf. VLANs werden standardmäßig gefiltert, um nur diejenigen anzuzeigen, die gültig sind. Damit ein VLAN gültig ist, muss es einer Infrastruktur zugeordnet sein, die einen Worker mit lokalem Plattenspeicher hosten kann.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks vlans --zone dal10
```
{: pre}

</br>


<br />


## Protokollierungsbefehle
{: #logging_commands}

### `ibmcloud ks apiserver-config-get audit-webhook`
{: #cs_apiserver_config_get}

Zeigt die URL für den fernen Protokollierungsservice an, an den Sie API-Serverauditprotokolle senden. Die URL wurde angegeben, als Sie das Webhook-Back-End für die API-Serverkonfiguration erstellt haben.
{: shortdesc}



```
ibmcloud ks apiserver-config-get audit-webhook --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>
</dl>

</br>

### `ibmcloud ks apiserver-config-set audit-webhook`
{: #cs_apiserver_config_set}

Legt das Webhook-Back-End für die API-Serverkonfiguration fest. Das Webhook-Back-End leitet API-Serverauditprotokolle an einen fernen Server weiter. Eine Webhook-Konfiguration wird auf der Grundlage der Informationen erstellt, die Sie in den Flags dieses Befehls bereitstellen. Wenn Sie keine Informationen in den Flags bereitstellen, wird eine Standard-Webhook-Konfiguration verwendet. Nach dem Festlegen des Webhooks müssen Sie den Befehl `ibmcloud ks apiserver-refresh` ausführen, um die Änderungen auf den Kubernetes-Master anzuwenden.
{: shortdesc}



```
ibmcloud ks apiserver-config-set audit-webhook --cluster CLUSTER [--remoteServer SERVER-URL_ODER_-IP] [--caCert PFAD_DES_CLIENTZERTIFIKATS] [--clientCert PFAD_DES_CLIENTZERTIFIKATS] [--clientKey PFAD_DES_CLIENTSCHLÜSSELS]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--remoteServer <em>SERVER-URL</em></code></dt>
<dd>Die URL oder IP-Adresse für den fernen Protokollierungsservice, an den Sie Auditprotokolle senden möchten. Wenn Sie eine unsichere Server-URL angeben, werden alle Zertifikate ignoriert. Dieser Wert ist optional.</dd>

<dt><code>--caCert <em>PFAD_DES_CA-ZERTIFIKATS</em></code></dt>
<dd>Der Dateipfad für das CA-Zertifikat, das zum Überprüfen des fernen Protokollierungsservice verwendet wird. Dieser Wert ist optional.</dd>

<dt><code>--clientCert <em>PFAD_DES_CLIENTZERTIFIKATS</em></code></dt>
<dd>Der Dateipfad des Clientzertifikats, das zum Authentifizieren beim fernen Protokollierungsservice verwendet wird. Dieser Wert ist optional.</dd>

<dt><code>--clientKey <em>PFAD_DES_CLIENTSCHLÜSSELS</em></code></dt>
<dd>Der Dateipfad für den entsprechenden Clientschlüssel, der zum Verbinden mit dem fernen Protokollierungsservice verwendet wird. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks apiserver-config-set audit-webhook --cluster mein_cluster --remoteServer https://audit.example.com/audit --caCert /mnt/etc/kubernetes/apiserver audit/ca.pem --clientCert /mnt/etc/kubernetes/apiserver audit/cert.pem --clientKey /mnt/etc/kubernetes/apiserver audit/key.pem
```
{: pre}

</br>
### `ibmcloud ks apiserver-config-unset audit-webhook`
{: #cs_apiserver_config_unset}

Inaktivieren Sie die Webhook-Back-End-Konfiguration für den API-Server des Clusters. Wenn Sie das Webhook-Back-End inaktivieren, wird die Weiterleitung von Auditprotokollen des API-Servers an einen fernen Server gestoppt.
{: shortdesc}



```
ibmcloud ks apiserver-config-unset audit-webhook --cluster CLUSTER
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>
</dl>

</br>

### `ibmcloud ks logging-autoupdate-disable`
{: #cs_log_autoupdate_disable}

Inaktiviert automatische Aktualisierungen aller Fluentd-Pods in einem Cluster.
{: shortdesc}



Inaktiviert die automatischen Aktualisierungen der Fluentd-Pods in einem bestimmten Cluster. Wenn Sie die Kubernetes-Hauptversion oder -Nebenversion Ihres Clusters aktualisieren, nimmt IBM automatisch die erforderlichen Änderungen an der Fluentd-Konfigurationszuordnung vor, ändert aber nicht die Buildversion Ihres Fluentd-Add-ons für die Protokollierung. Sie sind dafür verantwortlich, die Kompatibilität der aktuellen Kubernetes-Versionen und Ihrer Add-on-Images zu prüfen.

```
ibmcloud ks logging-autoupdate-disable --cluster CLUSTER
```
{: pre}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Sie automatische Aktualisierungen für das Fluentd-Add-on inaktivieren möchten. Dieser Wert ist erforderlich.</dd>
</dl>

</br>

### `ibmcloud ks logging-autoupdate-enable`
{: #cs_log_autoupdate_enable}

Aktiviert die automatischen Aktualisierungen für Ihre Fluentd-Pods in einem bestimmten Cluster. Fluentd-Pods werden automatisch aktualisiert, wenn eine neue Buildversion verfügbar ist.
{: shortdesc}



```
ibmcloud ks logging-autoupdate-enable --cluster CLUSTER
```
{: pre}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Sie automatische Aktualisierungen für das Fluentd-Add-on aktivieren möchten. Dieser Wert ist erforderlich.</dd>
</dl>

</br>

### `ibmcloud ks logging-autoupdate-get`
{: #cs_log_autoupdate_get}

Zeigt an, ob Ihre Fluentd-Pods so eingestellt sind, dass sie in einem Cluster automatisch aktualisiert werden.
{: shortdesc}



```
ibmcloud ks logging-autoupdate-get --cluster CLUSTER
```
{: pre}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Sie prüfen möchten, ob automatische Aktualisierungen für das Fluentd-Add-on aktiviert sind. Dieser Wert ist erforderlich.</dd>
</dl>

</br>

### `ibmcloud ks logging-collect`
{: #cs_log_collect}

Erstellt eine Anforderung für einen Snapshot der Protokolle zu einem bestimmten Zeitpunkt und speichert die Protokolle anschließend in einem {{site.data.keyword.cos_full_notm}}-Bucket.
{: shortdesc}



```
ibmcloud ks logging-collect --cluster CLUSTER --cos-bucket BUCKETNAME --cos-endpoint ENDPUNKT --hmac-key-id HMAC-SCHLÜSSEL-ID --hmac-key HMAC-SCHLÜSSEL --type PROTOKOLLTYP [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Sie einen Snapshot erstellen möchten.</dd>

<dt><code>--cos-bucket <em>BUCKETNAME</em></code></dt>
<dd>Der Name des {{site.data.keyword.cos_short}}-Buckets, in dem die Protokolle gespeichert werden sollen.</dd>

<dt><code>--cos-endpoint <em>ENDPUNKT</em></code></dt>
<dd>Der regionale, regionsübergreifende oder sich in einem einzelnen Rechenzentrum befindliche {{site.data.keyword.cos_short}}-Endpunkt für das Bucket, in dem die Protokolle gespeichert werden. Informationen zu verfügbaren Endpunkten finden Sie unter [Endpunkte und Speicherpositionen](/docs/services/cloud-object-storage/basics?topic=cloud-object-storage-endpoints) in der {{site.data.keyword.cos_short}}-Dokumentation.</dd>

<dt><code>--hmac-key-id <em>HMAC-SCHLÜSSEL-ID</em></code></dt>
<dd>Die eindeutige ID für die HMAC-Berechtigungsnachweise für die {{site.data.keyword.cos_short}}-Instanz.</dd>

<dt><code>--hmac-key <em>HMAC-SCHLÜSSEL</em></code></dt>
<dd>Der HMAC-Schlüssel für die {{site.data.keyword.cos_short}}-Instanz.</dd>

<dt><code>--type <em>PROTOKOLLTYP</em></code></dt>
<dd>Optional: Der Typ der Protokolle, für die ein Snapshot erstellt werden soll. Derzeit ist `master` die einzige Option und die Standardeinstellung.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispielbefehl**:

```
ibmcloud ks logging-collect --cluster mycluster --cos-bucket mybucket --cos-endpoint s3-api.us-geo.objectstorage.softlayer.net --hmac-key-id e2e7f5c9fo0144563c418dlhi3545m86 --hmac-key c485b9b9fo4376722f692b63743e65e1705301ab051em96j
```
{: pre}

**Beispielausgabe**:

```
There is no specified log type. The default master will be used.
Submitting log collection request for master logs for cluster mycluster...
  OK
  The log collection request was successfully submitted. To view the status of the request run ibmcloud ks logging-collect-status mycluster.
```
{: screen}

</br>
### `ibmcloud ks logging-collect-status`
{: #cs_log_collect_status}

Überprüft den Status der Snapshotanforderung für die Protokollerfassung im Cluster.
{: shortdesc}



```
ibmcloud ks logging-collect-status --cluster CLUSTER [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Administrator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Sie einen Snapshot erstellen möchten. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispielbefehl**:

```
ibmcloud ks logging-collect-status --cluster mycluster
```
{: pre}

**Beispielausgabe**:

```
Getting the status of the last log collection request for cluster mycluster...
  OK
  State     Start Time             Error   Log URLs
  success   2018-09-18 16:49 PDT   - s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-0-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-1-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
  s3-api.us-geo.objectstorage.softlayer.net/mybucket/master-2-0862ae70a9ae6c19845ba3pc0a2a6o56-1297318756.tgz
```
{: screen}

</br>
### `ibmcloud ks logging-config-create`
{: #cs_logging_create}

Erstellt eine Protokollierungskonfiguration. Sie können diesen Befehl verwenden, um Protokolle für Container, Anwendungen, Workerknoten, Kubernetes-Cluster und Ingress-Lastausgleichsfunktionen für Anwendungen an {{site.data.keyword.loganalysisshort_notm}} oder an einen externen Systemprotokollserver weiterzuleiten.
{: shortdesc}



```
ibmcloud ks logging-config-create --cluster CLUSTER --logsource PROTOKOLLQUELLE --type PROTOKOLLTYP [--namespace KUBERNETES-NAMENSBEREICH] [--hostname PROTOKOLLSERVER-HOSTNAME_ODER_-IP] [--port PROTOKOLLSERVER-PORT] [--space CLUSTERBEREICH] [--org CLUSTERORG] [--app-containers CONTAINER] [--app-paths PFAD_ZU_PROTOKOLLEN] [--syslog-protocol PROTOKOLL]  [--json] [--skip-validation] [--force-update][-s]
```
{: pre}

**Erforderliche Mindestberechtigungen**: Plattformrolle **Editor** für den Cluster für alle Protokollquellen außer `kube-audit` und Plattformrolle **Administrator** für den Cluster für die Protokollquelle `kube-audit`

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters.</dd>

<dt><code>--logsource <em>PROTOKOLLQUELLE</em></code></dt>
<dd>Die Protokollquelle, für die die Protokollweiterleitung aktiviert werden soll. Dieses Argument unterstützt eine durch Kommas getrennte Liste mit Protokollquellen, die auf die Konfiguration angewendet werden sollen. Gültige Werte sind <code>container</code>, <code>application</code>, <code>worker</code>, <code>kubernetes</code>, <code>storage</code>, <code>ingress</code> und <code>kube-audit</code>. Wenn Sie keine Protokollquelle bereitstellen, werden Konfigurationen für <code>container</code> und <code>ingress</code> erstellt.</dd>

<dt><code>--type <em>PROTOKOLLTYP</em></code></dt>
<dd>Gibt an, wohin Sie Ihre Protokolle weiterleiten möchten. Optionen sind <code>ibm</code>, wodurch Ihre Protokolle an {{site.data.keyword.loganalysisshort_notm}} weitergeleitet werden, und <code>syslog</code>, wodurch Ihre Protokolle an externe Server weitergeleitet werden.<p class="deprecated">{{site.data.keyword.loganalysisshort_notm}} wird nicht mehr verwendet. Diese Befehlsoption wird bis zum 30. September 2019 unterstützt.</p></dd>

<dt><code>--namespace <em>KUBERNETES-NAMENSBEREICH</em></code></dt>
<dd>Der Kubernetes-Namensbereich, von dem aus Protokolle weitergeleitet werden sollen. Die Weiterleitung von Protokollen wird für die Kubernetes-Namensbereiche <code>ibm-system</code> und <code>kube-system</code> nicht unterstützt. Dieser Wert ist nur für die Containerprotokollquelle gültig und optional. Wenn Sie keinen Namensbereich angeben, verwenden alle Namensbereiche im Cluster diese Konfiguration.</dd>

<dt><code>--hostname <em>PROTOKOLLSERVER-HOSTNAME</em></code></dt>
<dd>Wenn der Protokollierungstyp <code>syslog</code> lautet, gibt dieser Wert den Hostnamen oder die IP-Adresse des Protokollcollector-Servers an. Dieser Wert ist für <code>syslog</code> erforderlich. Wenn der Protokollierungstyp <code>ibm</code> lautet, gibt dieser Wert die {{site.data.keyword.loganalysislong_notm}}-Einpflege-URL an. Sie finden die Liste von verfügbaren Einpflege-URLs [hier](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls). Wenn Sie keine Einpflege-URL angeben, wird der Endpunkt für die Region, in der Ihr Cluster erstellt wurde, verwendet.</dd>

<dt><code>--port <em>PROTOKOLLSERVER-PORT</em></code></dt>
<dd>Der Port des Protokollcollector-Servers. Dieser Wert ist optional. Wenn Sie keinen Port angeben, wird der Standardport <code>514</code> für <code>syslog</code> und der Standardport <code>9091</code> für <code>ibm</code> verwendet.</dd>

<dt><code>--space <em>CLUSTERBEREICH</em></code></dt>
<dd>Optional: Der Name des Cloud Foundry-Bereichs, an den Sie die Protokolle senden möchten. Dieser Wert ist nur für den Protokolltyp <code>ibm</code> gültig und optional. Wenn Sie keinen Bereich angeben, werden Protokolle an die Kontoebene gesendet. Wenn Sie dies tun, müssen Sie auch eine Organisation (<code>org</code>) angeben.</dd>

<dt><code>--org <em>CLUSTERORG</em></code></dt>
<dd>Optional: Der Name der Cloud Foundry-Organisation, in der sich der Bereich befindet. Dieser Wert ist nur für den Protokolltyp <code>ibm</code> gültig und erforderlich, wenn Sie einen Bereich angegeben haben.</dd>

<dt><code>--app-paths</code></dt>
<dd>Der Pfad zu dem Container, an den die Apps Protokolle senden. Wenn Sie Protokolle mit dem Quellentyp <code>application</code> weiterleiten möchten, müssen Sie einen Pfad angeben. Wenn Sie mehr als einen Pfad angeben, verwenden Sie eine durch Kommas getrennte Liste. Dieser Wert ist für <code>application</code> der Protokollquelle erforderlich. Beispiel: <code>/var/log/myApp1/&ast;,/var/log/myApp2/&ast;</code></dd>

<dt><code>--syslog-protocol</code></dt>
<dd>Das Netzprotokoll (Transportschicht), das verwendet wird, wenn der Protokollierungstyp <code>syslog</code> lautet. Unterstützte Werte sind <code>tcp</code>, <code>tls</code> und der Standardwert <code>udp</code>. Bei einer Weiterleitung an einen rsyslog-Server mit dem <code>udp</code>-Protokoll werden Protokolle, die größer sind als 1 KB, abgeschnitten.</dd>

<dt><code>--app-containers</code></dt>
<dd>Zum Weiterleiten von Protokollen von Apps können Sie den Namen des Containers angeben, der Ihre App enthält. Sie können mehr als einen Container angeben, indem Sie eine durch Kommas getrennte Liste verwenden. Falls keine Container angegeben sind, werden Protokolle von allen Containern weitergeleitet, die die von Ihnen bereitgestellten Pfade enthalten. Diese Option ist nur für <code>application</code> der Protokollquelle gültig.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>--skip-validation</code></dt>
<dd>Überspringt die Validierung der Organisations- und Bereichsnamen, wenn sie angegeben werden. Das Überspringen der Validierung verringert die Bearbeitungszeit. Eine ungültige Protokollierungskonfiguration aber führt dazu, dass Protokolle nicht ordnungsgemäß weitergeleitet werden. Dieser Wert ist optional.</dd>

<dt><code>--force-update</code></dt>
<dd>Erzwingt eine Aktualisierung der Fluentd-Pods auf die aktuelle Version. Fluentd muss die aktuellste Version aufweisen, um Änderungen an den Protokollierungskonfigurationen vornehmen zu können.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiele**:

Beispiel für Protokolltyp `syslog` für Weiterleitung aus der Protokollquelle `container` am Standardport 514:
```
ibmcloud ks logging-config-create mein_cluster --logsource container --namespace mein_namensbereich  --hostname 169.xx.xxx.xxx --type syslog
```
{: pre}

Beispiel für Protokolltyp `syslog`, der Protokolle aus einer `ingress`-Quelle an einen anderen Port als den Standardport weiterleitet:
```
ibmcloud ks logging-config-create --cluster mein_cluster --logsource container --hostname 169.xx.xxx.xxx --port 5514 --type syslog
```
{: pre}

</br>
### `ibmcloud ks logging-config-get`
{: #cs_logging_get}

Zeigt alle Protokollweiterleitungskonfigurationen für einen Cluster an oder filtert die Protokollierungskonfigurationen auf Basis der Protokollquelle.
{: shortdesc}



```
ibmcloud ks logging-config-get --cluster CLUSTER [--logsource PROTOKOLLQUELLE] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--logsource <em>PROTOKOLLQUELLE</em></code></dt>
<dd>Die Art der Protokollquelle, für die die Filterung durchgeführt werden soll. Nur Protokollierungskonfigurationen dieser Protokollquelle im Cluster werden zurückgegeben. Gültige Werte sind <code>container</code>, <code>storage</code>, <code>application</code>, <code>worker</code>, <code>kubernetes</code> <code>ingress</code> und <code>kube-audit</code>. Dieser Wert ist optional.</dd>

<dt><code>--show-covering-filters</code></dt>
<dd>Zeigt die Protokollierungsfilter an, wodurch die vorherige Filter obsolet werden.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks logging-config-get --cluster mein_cluster --logsource worker
```
{: pre}

</br>
### `ibmcloud ks logging-config-refresh`
{: #cs_logging_refresh}

Aktualisiert die Protokollierungskonfiguration für den Cluster. Durch diese Aktion wird das Protokollierungstoken für alle Protokollierungskonfigurationen aktualisiert, bei denen die Weiterleitung an die Bereichsebene in Ihrem Cluster erfolgt.
{: shortdesc}



```
ibmcloud ks logging-config-refresh --cluster CLUSTER [--force-update] [-s]
```

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--force-update</code></dt>
<dd>Erzwingt eine Aktualisierung der Fluentd-Pods auf die aktuelle Version. Fluentd muss die aktuellste Version aufweisen, um Änderungen an den Protokollierungskonfigurationen vornehmen zu können.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:

  ```
  ibmcloud ks logging-config-refresh --cluster mein_cluster
  ```
  {: pre}

</br>
### `ibmcloud ks logging-config-rm`
{: #cs_logging_rm}

Löscht eine Protokollweiterleitungskonfiguration oder alle Protokollierungskonfigurationen für einen Cluster. Durch die Löschung der Protokollkonfiguration wird die Protokollweiterleitung an einen fernen Systemprotokollserver bzw. an {{site.data.keyword.loganalysisshort_notm}} gestoppt.
{: shortdesc}



```
ibmcloud ks logging-config-rm --cluster CLUSTER [--id PROTOKOLLKONFIGURATIONS-ID] [--all] [--force-update] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen**: Plattformrolle **Editor** für den Cluster für alle Protokollquellen außer `kube-audit` und Plattformrolle **Administrator** für den Cluster für die Protokollquelle `kube-audit`

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--id <em>PROTOKOLLKONFIGURATIONS-ID</em></code></dt>
<dd>Wenn Sie eine einzelne Protokollierungskonfiguration entfernen möchten, die ID der Protokollierungskonfiguration.</dd>

<dt><code>--all</code></dt>
<dd>Das Flag zum Entfernen aller Protokollierungskonfigurationen in einem Cluster.</dd>

<dt><code>--force-update</code></dt>
<dd>Erzwingt eine Aktualisierung der Fluentd-Pods auf die aktuelle Version. Fluentd muss die aktuellste Version aufweisen, um Änderungen an den Protokollierungskonfigurationen vornehmen zu können.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks logging-config-rm --cluster mein_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e
```
{: pre}

</br>
### `ibmcloud ks logging-config-update`
{: #cs_logging_update}

Aktualisiert die Details einer Protokollweiterleitungskonfiguration.
{: shortdesc}



```
ibmcloud ks logging-config-update --cluster CLUSTER --id PROTOKOLLKONFIGURATIONS-ID --type PROTOKOLLTYP  [--namespace NAMENSBEREICH] [--hostname PROTOKOLLSERVER-HOSTNAME_ODER_-IP] [--port PROTOKOLLSERVER-PORT] [--space CLUSTERBEREICH] [--org CLUSTERORG] [--app-paths PFAD] [--app-containers PFAD] [--json] [--skipValidation] [--force-update] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--id <em>PROTOKOLLKONFIGURATIONS-ID</em></code></dt>
<dd>Die ID der Protokollierungskonfiguration, die aktualisiert werden soll. Dieser Wert ist erforderlich.</dd>

<dt><code>--type <em>PROTOKOLLTYP</em></code></dt>
<dd>Das Protokollweiterleitungsprotokoll, das Sie verwenden möchten. Momentan werden <code>syslog</code> und <code>ibm</code> unterstützt. Dieser Wert ist erforderlich.</dd>

<dt><code>--namespace <em>NAMENSBEREICH</em></code>
<dd>Der Kubernetes-Namensbereich, von dem aus Protokolle weitergeleitet werden sollen. Die Weiterleitung von Protokollen wird für die Kubernetes-Namensbereiche <code>ibm-system</code> und <code>kube-system</code> nicht unterstützt. Dieser Wert ist nur für die Protokollquelle <code>container</code> gültig. Wenn Sie keinen Namensbereich angeben, verwenden alle Namensbereiche im Cluster diese Konfiguration.</dd>

<dt><code>--hostname <em>PROTOKOLLSERVER-HOSTNAME</em></code></dt>
<dd>Wenn der Protokollierungstyp <code>syslog</code> lautet, gibt dieser Wert den Hostnamen oder die IP-Adresse des Protokollcollector-Servers an. Dieser Wert ist für <code>syslog</code> erforderlich. Wenn der Protokollierungstyp <code>ibm</code> lautet, gibt dieser Wert die {{site.data.keyword.loganalysislong_notm}}-Einpflege-URL an. Sie finden die Liste von verfügbaren Einpflege-URLs [hier](/docs/services/CloudLogAnalysis?topic=cloudloganalysis-log_ingestion#log_ingestion_urls). Wenn Sie keine Einpflege-URL angeben, wird der Endpunkt für die Region, in der Ihr Cluster erstellt wurde, verwendet.</dd>

<dt><code>--port <em>PROTOKOLLSERVER-PORT</em></code></dt>
<dd>Der Port des Protokollcollector-Servers. Dieser Wert ist optional, wenn der Protokollierungstyp <code>syslog</code> lautet. Wenn Sie keinen Port angeben, wird der Standardport <code>514</code> für <code>syslog</code> und <code>9091</code> für <code>ibm</code> verwendet.</dd>

<dt><code>--space <em>CLUSTERBEREICH</em></code></dt>
<dd>Optional: Der Name des Bereichs, an den die Protokolle gesendet werden sollen. Dieser Wert ist nur für den Protokolltyp <code>ibm</code> gültig und optional. Wenn Sie keinen Bereich angeben, werden Protokolle an die Kontoebene gesendet. Wenn Sie dies tun, müssen Sie auch eine Organisation (<code>org</code>) angeben.</dd>

<dt><code>--org <em>CLUSTERORG</em></code></dt>
<dd>Optional: Der Name der Cloud Foundry-Organisation, in der sich der Bereich befindet. Dieser Wert ist nur für den Protokolltyp <code>ibm</code> gültig und erforderlich, wenn Sie einen Bereich angegeben haben.</dd>

<dt><code>--app-paths <em>PFAD</em>,<em>PFAD</em></code></dt>
<dd>Ein absoluter Dateipfad in dem Container, aus dem Protokolle erfasst werden. Platzhalter, wie '/var/log/*.log', können zwar verwendet werden, nicht jedoch rekursive Globale, wie '/var/log/**/test.log'. Wenn Sie mehr als einen Pfad angeben, verwenden Sie eine durch Kommas getrennte Liste. Dieser Wert ist erforderlich, wenn Sie 'application' für die Protokollquelle angeben. </dd>

<dt><code>--app-containers <em>PFAD</em>,<em>PFAD</em></code></dt>
<dd>Der Pfad für die Container, in die die Apps die Protokolle schreiben. Wenn Sie Protokolle mit dem Quellentyp <code>application</code> weiterleiten möchten, müssen Sie einen Pfad angeben. Wenn Sie mehr als einen Pfad angeben, verwenden Sie eine durch Kommas getrennte Liste. Beispiel: <code>/var/log/myApp1/&ast;,/var/log/myApp2/&ast;</code></dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>--skipValidation</code></dt>
<dd>Überspringt die Validierung der Organisations- und Bereichsnamen, wenn sie angegeben werden. Das Überspringen der Validierung verringert die Bearbeitungszeit. Eine ungültige Protokollierungskonfiguration aber führt dazu, dass Protokolle nicht ordnungsgemäß weitergeleitet werden. Dieser Wert ist optional.</dd>

<dt><code>--force-update</code></dt>
<dd>Erzwingt eine Aktualisierung der Fluentd-Pods auf die aktuelle Version. Fluentd muss die aktuellste Version aufweisen, um Änderungen an den Protokollierungskonfigurationen vornehmen zu können.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel für Protokolltyp `ibm`**:

  ```
  ibmcloud ks logging-config-update mein_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e --type ibm
  ```
  {: pre}

**Beispiel für Protokolltyp `syslog`**:

  ```
  ibmcloud ks logging-config-update --cluster mein_cluster --id f4bc77c0-ee7d-422d-aabf-a4e6b977264e --hostname localhost --port 5514 --type syslog
  ```
  {: pre}

</br>
### `ibmcloud ks logging-filter-create`
{: #cs_log_filter_create}

Filtert Protokolle heraus, die durch Ihre Protokollierungskonfiguration weitergeleitet werden.
{: shortdesc}



```
ibmcloud ks logging-filter-create --cluster CLUSTER --type PROTOKOLLTYP [--logging-configs KONFIGURATIONEN] [--namespace KUBERNETES-NAMENSBEREICH] [--container CONTAINERNAME] [--level PROTOKOLLIERUNGSSTUFE] [--message NACHRICHT] [--regex-message NACHRICHT] [--force-update] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Sie einen Protokollierungsfilter erstellen möchten. Dieser Wert ist erforderlich.</dd>

<dt><code>--type <em>PROTOKOLLTYP</em></code></dt>
<dd>Der Typ von Protokollen, auf die Sie den Filter anwenden möchten. Momentan werden <code>all</code>, <code>container</code> und <code>host</code> unterstützt.</dd>

<dt><code>--logging-configs <em>KONFIGURATIONEN</em></code></dt>
<dd>Eine durch Kommas getrennte Liste Ihrer Protokollierungskonfigurations-IDs. Wird sie nicht bereitgestellt, wird der Filter auf alle Clusterprotokollierungskonfigurationen angewendet, die an den Filter übergeben werden. Sie können mit dem Filter übereinstimmende Protokollkonfigurationen anzeigen, indem Sie das Flag <code>--show-matching-configs</code> mit dem Befehl verwenden. Dieser Wert ist optional.</dd>

<dt><code>--namespace <em>KUBERNETES-NAMENSBEREICH</em></code></dt>
<dd>Der Kubernetes-Namensbereich, in dem Sie Protokolle filtern möchten. Dieser Wert ist optional.</dd>

<dt><code>--container <em>CONTAINERNAME</em></code></dt>
<dd>Der Name des Containers, in dem Sie Protokolle filtern möchten. Dieses Flag ist nur mit dem Protokolltyp <code>container</code> anwendbar. Dieser Wert ist optional.</dd>

<dt><code>--level <em>PROTOKOLLIERUNGSSTUFE</em></code></dt>
<dd>Filtert Protokolle auf einer angegebenen Stufe oder den darunterliegenden Stufen heraus. Zulässige Werte in ihrer kanonischen Reihenfolge sind <code>fatal</code>, <code>error</code>, <code>warn/warning</code>, <code>info</code>, <code>debug</code> und <code>trace</code>. Dieser Wert ist optional. Beispiel: Wenn Sie Protokolle auf der Stufe <code>info</code> filtern, wird auch auf den Stufen <code>debug</code> und <code>trace</code> gefiltert. **Hinweis**: Sie können dieses Flag nur dann verwenden, wenn Protokollnachrichten das JSON-Format aufweisen und ein Feld für die Stufe enthalten. Beispielausgabe: <code>{"log": "hello", "level": "info"}</code></dd>

<dt><code>--message <em>NACHRICHT</em></code></dt>
<dd>Filtert alle Protokolle mit einer bestimmten Nachricht heraus. Dieser Wert ist optional. Beispiel: Die Nachrichten "Hello", "!"und "Hello, World!"würden im Protokoll "Hello, World!" wiedergefunden.</dd>

<dt><code>--regex-message <em>NACHRICHT</em></code></dt>
<dd>Optional: Filtert alle Protokolle heraus, die eine angegebene Nachricht enthalten, die als regulärer Ausdruck an einer beliebigen Stelle im Protokoll geschrieben wird. Dieser Wert ist optional. Beispiel: Das Muster "hello [0-9]" würde auf "hello 1", "hello 2" und "hello 9" angewendet werden.</dd>

<dt><code>--force-update</code></dt>
<dd>Erzwingt eine Aktualisierung der Fluentd-Pods auf die aktuelle Version. Fluentd muss die aktuellste Version aufweisen, um Änderungen an den Protokollierungskonfigurationen vornehmen zu können.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiele**:

In diesem Beispiel werden alle Protokolle herausgefiltert, die von Containern mit dem Namen `test-container` im Standardnamensbereich weitergeleitet werden, die sich auf der Stufe 'debug' oder einer niedrigeren Stufe befinden und eine Protokollnachricht haben, die 'GET request' enthält.
```
ibmcloud ks logging-filter-create --cluster example-cluster --type container --namespace default --container test-container --level debug --message "GET request"
```
{: pre}

Im folgenden Beispiel werden alle Protokolle herausgefiltert, die von einem bestimmten Cluster auf der Stufe <code>info</code> oder einer niedrigeren Stufe weitergeleitet werden. Die Ausgabe wird als JSON zurückgegeben.
```
ibmcloud ks logging-filter-create --cluster example-cluster --type all --level info --json
```
{: pre}

</br>
### `ibmcloud ks logging-filter-get`
{: #cs_log_filter_view}

Zeigt eine Protokollierungsfilterkonfiguration an.
{: shortdesc}



```
ibmcloud ks logging-filter-get --cluster CLUSTER [--id FILTER-ID] [--show-matching-configs] [--show-covering-filters] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für das Sie Filter anzeigen möchten. Dieser Wert ist erforderlich.</dd>

<dt><code>--id <em>FILTER-ID</em></code></dt>
<dd>Die ID des Protokollfilters, den Sie anzeigen möchten.</dd>

<dt><code>--show-matching-configs</code></dt>
<dd>Zeigt die Protokollierungskonfigurationen an, die mit der überprüften Konfiguration übereinstimmen. Dieser Wert ist optional.</dd>

<dt><code>--show-covering-filters</code></dt>
<dd>Zeigt die Protokollierungsfilter an, wodurch die vorherigen Filter obsolet werden. Dieser Wert ist optional.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks logging-filter-get --cluster mycluster --id 885732 --show-matching-configs
```
{: pre}

</br>
### `ibmcloud ks logging-filter-rm`
{: #cs_log_filter_delete}

Löscht einen Protokollierungsfilter.
{: shortdesc}



```
ibmcloud ks logging-filter-rm --cluster CLUSTER [--id FILTER-ID] [--all] [--force-update] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, aus dem Sie einen Protokollierungsfilter löschen möchten.</dd>

<dt><code>--id <em>FILTER-ID</em></code></dt>
<dd>Die ID des Protokollfilters, der gelöscht werden soll.</dd>

<dt><code>--all</code></dt>
<dd>Löscht alle Protokollweiterleitungsfilter. Dieser Wert ist optional.</dd>

<dt><code>--force-update</code></dt>
<dd>Erzwingt eine Aktualisierung der Fluentd-Pods auf die aktuelle Version. Fluentd muss die aktuellste Version aufweisen, um Änderungen an den Protokollierungskonfigurationen vornehmen zu können.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks logging-filter-rm --cluster mycluster --id 885732
```
{: pre}

</br>
### `ibmcloud ks logging-filter-update`
{: #cs_log_filter_update}

Aktualisiert einen Protokollierungsfilter.
{: shortdesc}



```
ibmcloud ks logging-filter-update --cluster CLUSTER --id FILTER-ID --type PROTOKOLLTYP [--logging-configs KONFIGURATIONEN] [--namespace KUBERNETES-NAMENSBEREICH] [--container CONTAINERNAME] [--level PROTOKOLLIERUNGSSTUFE] [--message NACHRICHT] [--regex-message NACHRICHT] [--force-update] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Sie einen Protokollierungsfilter aktualisieren möchten. Dieser Wert ist erforderlich.</dd>

<dt><code>--id <em>FILTER-ID</em></code></dt>
<dd>Die ID des Protokollfilters, der aktualisiert werden soll.</dd>

<dt><code>--type <em>PROTOKOLLTYP</em></code></dt>
<dd>Der Typ von Protokollen, auf die Sie den Filter anwenden möchten. Momentan werden <code>all</code>, <code>container</code> und <code>host</code> unterstützt.</dd>

<dt><code>--logging-configs <em>KONFIGURATIONEN</em></code></dt>
<dd>Eine durch Kommas getrennte Liste Ihrer Protokollierungskonfigurations-IDs. Wird sie nicht bereitgestellt, wird der Filter auf alle Clusterprotokollierungskonfigurationen angewendet, die an den Filter übergeben werden. Sie können mit dem Filter übereinstimmende Protokollkonfigurationen anzeigen, indem Sie das Flag <code>--show-matching-configs</code> mit dem Befehl verwenden. Dieser Wert ist optional.</dd>

<dt><code>--namespace <em>KUBERNETES-NAMENSBEREICH</em></code></dt>
<dd>Der Kubernetes-Namensbereich, in dem Sie Protokolle filtern möchten. Dieser Wert ist optional.</dd>

<dt><code>--container <em>CONTAINERNAME</em></code></dt>
<dd>Der Name des Containers, in dem Sie Protokolle filtern möchten. Dieses Flag ist nur mit dem Protokolltyp <code>container</code> anwendbar. Dieser Wert ist optional.</dd>

<dt><code>--level <em>PROTOKOLLIERUNGSSTUFE</em></code></dt>
<dd>Filtert Protokolle auf einer angegebenen Stufe oder den darunterliegenden Stufen heraus. Zulässige Werte in ihrer kanonischen Reihenfolge sind <code>fatal</code>, <code>error</code>, <code>warn/warning</code>, <code>info</code>, <code>debug</code> und <code>trace</code>. Dieser Wert ist optional. Beispiel: Wenn Sie Protokolle auf der Stufe <code>info</code> filtern, wird auch auf den Stufen <code>debug</code> und <code>trace</code> gefiltert. **Hinweis**: Sie können dieses Flag nur dann verwenden, wenn Protokollnachrichten das JSON-Format aufweisen und ein Feld für die Stufe enthalten. Beispielausgabe: <code>{"log": "hello", "level": "info"}</code></dd>

<dt><code>--message <em>NACHRICHT</em></code></dt>
<dd>Filtert alle Protokolle mit einer bestimmten Nachricht heraus. Dieser Wert ist optional. Beispiel: Die Nachrichten "Hello", "!"und "Hello, World!"würden im Protokoll "Hello, World!" wiedergefunden.</dd>

<dt><code>--regex-message <em>NACHRICHT</em></code></dt>
<dd>Optional: Filtert alle Protokolle heraus, die eine angegebene Nachricht enthalten, die als regulärer Ausdruck an einer beliebigen Stelle im Protokoll geschrieben wird. Dieser Wert ist optional. Beispiel: Das Muster "hello [0-9]" würde auf "hello 1", "hello 2" und "hello 9" angewendet werden.</dd>

<dt><code>--force-update</code></dt>
<dd>Erzwingt eine Aktualisierung der Fluentd-Pods auf die aktuelle Version. Fluentd muss die aktuellste Version aufweisen, um Änderungen an den Protokollierungskonfigurationen vornehmen zu können.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiele**:

In diesem Beispiel werden alle Protokolle herausgefiltert, die von Containern mit dem Namen `test-container` im Standardnamensbereich weitergeleitet werden, die sich auf der Stufe 'debug' oder einer niedrigeren Stufe befinden und eine Protokollnachricht haben, die 'GET request' enthält.
```
ibmcloud ks logging-filter-update --cluster example-cluster --id 885274 --type container --namespace default --container test-container --level debug --message "GET request"
```
{: pre}

Im folgenden Beispiel werden alle Protokolle herausgefiltert, die von einem bestimmten Cluster auf der Stufe <code>info</code> oder einer niedrigeren Stufe weitergeleitet werden. Die Ausgabe wird als JSON zurückgegeben.
```
ibmcloud ks logging-filter-update --cluster example-cluster --id 274885 --type all --level info --json
```
{: pre}

<br />


## Befehle der Netzlastausgleichsfunktion (NLB)
{: #nlb-dns}

Verwenden Sie diese Befehlsgruppe zum Erstellen und Verwalten von Hostnamen für IP-Adressen der Netzlastausgleichsfunktion (NLB) und Statusprüfmonitore für Hostnamen. Weitere Informationen finden Sie unter [Hostnamen für Lastausgleichsfunktion registrieren](/docs/containers?topic=containers-loadbalancer_hostname).
{: shortdesc}



### `ibmcloud ks nlb-dns-add`
{: #cs_nlb-dns-add}

Fügt eine NLB-IP (NLB = Network Load Balancer) zu einem vorhandenen Hostnamen hinzu, den Sie mit dem [Befehl `ibmcloud ks nlb-dns-create`](#cs_nlb-dns-create) erstellt haben.
{: shortdesc}



In einem Mehrzonencluster können Sie beispielsweise in jeder Zone eine NLB bereitstellen, um eine App zugänglich zu machen. Sie registrieren eine NLB-IP in einer Zone mit einem Hostnamen, indem Sie `ibmcloud ks nlb-dns-create` ausführen, sodass Sie nun die NLB-IPs aus den anderen Zonen zu diesem vorhandenen Hostnamen hinzufügen können. Wenn ein Benutzer auf den Hostnamen Ihrer App zugreift, greift der Client zufällig auf eine dieser IPs zu und die Anforderung wird an diese NLB gesendet. Sie müssen den folgenden Befehl für jede IP-Adresse ausführen, die hinzugefügt werden soll.

```
ibmcloud ks nlb-dns-add --cluster CLUSTER --ip IP --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>Die NLB-IP, die dem Hostnamen hinzugefügt werden soll. Um Ihre NLB-IPs anzuzeigen, führen Sie <code>kubectl get svc</code> aus.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Der Hostname, dem Sie IPs hinzufügen möchten. Zum Anzeigen der vorhandenen Hostnamen führen Sie den Befehl <code>ibmcloud ks nlb-dnss</code> aus.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-add --cluster mycluster --ip 1.1.1.1 --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud ks nlb-dns-create`
{: #cs_nlb-dns-create}

Machen Sie Ihre App öffentlich zugänglich, indem Sie einen DNS-Hostnamen erstellen, der eine NLB-IP (NLB) registriert.
{: shortdesc}



```
ibmcloud ks nlb-dns-create --cluster CLUSTER --ip IP [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>Die IP-Adresse der Netzlastausgleichsfunktion, die registriert werden soll. Um Ihre NLB-IPs anzuzeigen, führen Sie <code>kubectl get svc</code> aus. Zunächst können Sie den Hostnamen mit nur einer IP-Adresse erstellen. Wenn ein Mehrzonenclusterin jeder Zone NLBs enthält, die eine App bereitstellen, können Sie die IPs der anderen NLBs zum Hostnamen hinzufügen, indem Sie den Befehl [`ibmcloud ks nlb-dns-add`](#cs_nlb-dns-add) ausführen.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-create --cluster mycluster --ip 1.1.1.1
```
{: pre}

</br>
### `ibmcloud ks nlb-dns-rm`
{: #cs_nlb-dns-rm}

NLB-IP-Adresse aus einem Hostnamen entfernen. Wenn Sie alle IPs aus einem Hostnamen entfernen, ist der Hostname immer noch vorhanden, nur sind ihm keine IPs zugeordnet. <strong>Hinweis</strong>: Sie müssen diesen Befehl für jede IP-Adresse ausführen, die entfernt werden soll.
{: shortdesc}



```
ibmcloud ks nlb-dns-rm --cluster CLUSTER --ip IP --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--ip <em>IP</em></code></dt>
<dd>Die NLB-IP, die entfernt werden soll. Um Ihre NLB-IPs anzuzeigen, führen Sie <code>kubectl get svc</code> aus.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Der Hostname, aus dem eine IP entfernt werden soll. Zum Anzeigen der vorhandenen Hostnamen führen Sie den Befehl <code>ibmcloud ks nlb-dnss</code> aus.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-rm --cluster mycluster --ip 1.1.1.1 --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud ks nlb-dnss`
{: #cs_nlb-dns-ls}

NLB-Hostnamen und -IP-Adressen auflisten, die in einem Cluster registriert sind.
{: shortdesc}



```
ibmcloud ks nlb-dnss --cluster CLUSTER [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dnss --cluster mycluster
```
{: pre}

</br>
### `ibmcloud ks nlb-dns-monitor-configure`
{: #cs_nlb-dns-monitor-configure}

Statusprüfmonitor für einen vorhandenen NLB-Hostnamen in einem Cluster konfigurieren und optional aktivieren. Wenn Sie einen Monitor für Ihren Hostnamen aktivieren, wird damit die NLB-IP in jeder Zone überwacht und die Ergebnisse der DNS-Suche werden auf Grundlage dieser Statusprüfungen aktualisiert.
{: shortdesc}

Mit diesem Befehl können Sie einen neuen Statusprüfmonitor erstellen und aktivieren oder die Einstellungen für einen vorhandenen Statusprüfmonitor aktualisieren. Zum Erstellen eines neuen Monitors schließen Sie das Flag `--enable` sowie die Flags für alle Einstellungen ein, die Sie konfigurieren möchten. Zum Aktualisieren eines vorhandenen Monitors müssen Sie nur die Flags für die Einstellungen angeben, die geändert werden sollen.



```
ibmcloud ks nlb-dns-monitor-configure --cluster CLUSTER --nlb-host HOST NAME [--enable] [--desc DESCRIPTION] [--type TYPE] [--method METHOD] [--path PATH] [--timeout TIMEOUT] [--retries RETRIES] [--interval INTERVAL] [--port PORT] [--header HEADER] [--expected-body BODY STRING] [--expected-codes HTTP CODES] [--follows-redirects TRUE] [--allows-insecure TRUE] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, in dem der Hostname registriert ist.</dd>

<dt><code>--nlb-host <em>HOST NAME</em></code></dt>
<dd>Der Hostname, für den ein Statusprüfmonitor konfiguriert werden soll. Zum Auflisten der Hostnamen führen Sie den Befehl <code>ibmcloud ks nlb-dnss --cluster CLUSTER</code> aus.</dd>

<dt><code>--enable</code></dt>
<dd>Schließen Sie dieses Flag ein, um einen neuen Statusprüfmonitor für einen Hostnamen zu erstellen und zu aktivieren.</dd>

<dt><code>--description <em>DESCRIPTION</em></code></dt>
<dd>Eine Beschreibung des Statusprüfmonitors.</dd>

<dt><code>--type <em>TYPE</em></code></dt>
<dd>Das für die Statusprüfung zu verwendende Protokoll: <code>HTTP</code>, <code>HTTPS</code> oder <code>TCP</code>. Standardwert: <code>HTTP</code></dd>

<dt><code>--method <em>METHOD</em></code></dt>
<dd>Die für die Statusprüfung zu verwendende Methode. Standardwert für <code>type</code> <code>HTTP</code> und <code>HTTPS</code>: <code>GET</code>. Standardwert für <code>type</code> <code>TCP</code>: <code>connection_established</code>.</dd>

<dt><code>--path <em>PATH</em></code></dt>
<dd>Wenn <code>type</code> auf <code>HTTPS</code> festgelegt ist: der Endpunktpfad, anhand dessen die Statusprüfung erfolgt. Standardwert: <code>/</code></dd>

<dt><code>--timeout <em>TIMEOUT</em></code></dt>
<dd>Das Zeitlimit in Sekunden, bevor die IP-Adresse als nicht erreichbar eingestuft wird. Die Statusprüfung wartet die im Parameter `interval` angegebene Anzahl von Sekunden, bevor erneut versucht wird, die IP zu erreichen. Der Wert muss eine ganze Zahl im Bereich zwischen 1 und 15 sein. Standardwert: <code>5</code></dd>

<dt><code>--retries <em>RETRIES</em></code></dt>
<dd>Bei einer Zeitlimitüberschreitung ist dies die Anzahl der Versuche, bis die nicht erreichbare IP als fehlerhaft eingestuft wird. Neuversuche werden sofort ausgeführt. Der Wert muss eine ganze Zahl im Bereich zwischen 1 und 5 sein. Standardwert: <code>2</code></dd>

<dt><code>--interval <em>INTERVAL</em></code></dt>
<dd>Das Intervall (in Sekunden) zwischen den einzelnen Statusprüfungen. Kurze Intervalle können die Failover-Zeit verbessern, erhöhen allerdings die Auslastung der IPs. Der Wert muss eine ganze Zahl im Bereich zwischen 10 und 3600 sein und er muss größer als `(WIEDERHOLUNGEN + 1) * ZEITLIMIT` sein. Standardwert: <code>60</code></dd>

<dt><code>--port <em>PORT</em></code></dt>
<dd>Die Portnummer, zu der eine Verbindung zwecks Statusprüfung hergestellt werden soll. Wenn <code>type</code> auf <code>TCP</code> gesetzt ist, ist dieser Parameter erforderlich. Wenn <code>type</code> auf <code>HTTP</code> oder <code>HTTPS</code> gesetzt ist, definieren Sie den Port nur dann, wenn Sie einen anderen Port als Port 80 für HTTP bzw. 443 für HTTPS verwenden. Standardwert für TCP: <code>0</code>. Standardwert für HTTP: <code>80</code>. Standardwert für HTTPS: <code>443</code>.</dd>

<dt><code>--header <em>HEADER</em></code></dt>
<dd>Wenn <code>type</code> auf <code>HTTPS</code> oder <code>HTTPS</code> gesetzt ist: Die bei der Statusprüfung zu sendenden HTTP-Anforderungsheader, z. B. der Host-Header. Der Benutzeragentenheader (User-Agent) kann nicht überschrieben werden.</dd>

<dt><code>--expected-body <em>BODY STRING</em></code></dt>
<dd>Wenn <code>type</code> auf <code>HTTP</code> oder <code>HTTPS</code> gesetzt ist: eine Unterzeichenfolge ohne Beachtung der Groß-/Kleinschreibung, nach der die Statusprüfung im Antworthauptteil sucht. Wenn diese Zeichenfolge nicht gefunden wird, wird die IP-Adresse als fehlerhaft eingestuft.</dd>

<dt><code>--expected-codes <em>HTTP CODES</em></code></dt>
<dd>Wenn <code>type</code> auf <code>HTTP</code> oder <code>HTTPS</code> gesetzt ist: HTTP-Codes, nach denen die Statusprüfung in der Antwort sucht. Wenn der HTTP-Code nicht gefunden wird, wird die IP-Adresse als fehlerhaft eingestuft. Standardwert: <code>2xx</code></dd>

<dt><code>--allows-insecure <em>TRUE</em></code></dt>
<dd>Wenn <code>type</code> auf <code>HTTP</code> oder <code>HTTPS</code> gesetzt ist: auf <code>true</code> setzen, damit das Zertifikat nicht validiert wird.</dd>

<dt><code>--follows-redirects <em>TRUE</em></code></dt>
<dd>Wenn <code>type</code> auf <code>HTTP</code> oder <code>HTTPS</code> gesetzt ist: auf <code>true</code> setzen, um allen Weiterleitungen zu folgen, die von der IP zurückgegeben werden.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-monitor-configure --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud --enable --desc "Login page monitor" --type HTTPS --method GET --path / --timeout 5 --retries 2 --interval 60  --expected-body "healthy" --expected-codes 2xx --follows-redirects true
```
{: pre}

</br>
### `ibmcloud ks nlb-dns-monitor-disable`
{: #cs_nlb-dns-monitor-disable}

Vorhandenen Statusprüfmonitor für einen Hostnamen in einem Cluster inaktivieren.
{: shortdesc}



```
ibmcloud ks nlb-dns-monitor-disable --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Der Hostname, der vom Zustandsmonitor geprüft wird. Zum Auflisten der Hostnamen führen Sie den Befehl <code>ibmcloud ks nlb-dnss --cluster CLUSTER</code> aus.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-monitor-disable --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>
### `ibmcloud ks nlb-dns-monitor-enable`
{: #cs_nlb-dns-monitor-enable}

Einen von Ihnen konfigurierten Statusprüfmonitor aktivieren.
{: shortdesc}

Wenn Sie zum ersten Mal einen Statusprüfmonitor erstellen, müssen Sie ihn mit dem Befehl `ibmcloud ks nlb-dns-monitor-configure` konfigurieren und aktivieren. Verwenden Sie den Befehl `ibmcloud ks nlb-dns-monitor-enable` nur, um einen Monitor zu aktivieren, den Sie konfiguriert, aber noch nicht aktiviert haben, oder um einen Monitor neu zu aktivieren, den Sie zuvor inaktiviert haben.



```
ibmcloud ks nlb-dns-monitor-enable --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Der Hostname, der vom Zustandsmonitor geprüft wird. Zum Auflisten der Hostnamen führen Sie den Befehl <code>ibmcloud ks nlb-dnss --cluster CLUSTER</code> aus.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-monitor-enable --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>

### `ibmcloud ks nlb-dns-monitor-get`
{: #cs_nlb-dns-monitor-get}

Einstellungen für einen vorhandenen Statusprüfmonitor anzeigen.
{: shortdesc}



```
ibmcloud ks nlb-dns-monitor-get --cluster CLUSTER --nlb-host HOST_NAME [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Der Hostname, der vom Zustandsmonitor geprüft wird. Zum Auflisten der Hostnamen führen Sie den Befehl <code>ibmcloud ks nlb-dnss --cluster CLUSTER</code> aus.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-monitor-get --cluster mycluster --nlb-host mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud
```
{: pre}

</br>

### `ibmcloud ks nlb-dns-monitor-status`
{: #cs_nlb-dns-monitor-status}

Status der Statusprüfung für die IPs hinter den NLB-Hostnamen in einem Cluster auflisten.
{: shortdesc}



```
ibmcloud ks nlb-dns-monitor-status --cluster CLUSTER [--nlb-host HOSTNAME] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--nlb-host <em>HOST_NAME</em></code></dt>
<dd>Schließen Sie dieses Flag ein, um den Status für nur einen Hostnamen anzuzeigen. Zum Auflisten der Hostnamen führen Sie den Befehl <code>ibmcloud ks nlb-dnss --cluster CLUSTER</code> aus.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-monitor-status --cluster mycluster
```
{: pre}

</br>
### `ibmcloud ks nlb-dns-monitors`
{: #cs_nlb-dns-monitor-ls}

Einstellungen des Statusprüfmonitors für jeden NLB-Hostnamen in einem Cluster auflisten.
{: shortdesc}



```
ibmcloud ks nlb-dns-monitors --cluster CLUSTER [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Editor** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks nlb-dns-monitors --cluster mycluster
```
{: pre}

<br />


## Regions- und Standortbefehle
{: #region_commands}

Verwenden Sie diese Befehlsgruppe, um verfügbare Positionen oder die aktuell als Ziel angegebene Region anzuzeigen und um eine Region als Ziel festzulegen.
{: shortdesc}

### Veraltet: `ibmcloud ks region-get`
{: #cs_region}

Nach der {{site.data.keyword.containerlong_notm}}-Region suchen, die aktuell Ihr Ziel ist.
{: shortdesc}

Sie können mit Ressourcen arbeiten, auf die Sie an jedem beliebigen Standort Zugriff haben, selbst wenn Sie durch Ausführen von `ibmcloud ks region-set` eine Region festlegen und die Ressource, mit der Sie arbeiten möchten, sich in einer anderen Region befindet. Wenn Sie Cluster mit demselben Namen in verschiedenen Regionen haben, können Sie entweder die Cluster-ID verwenden, wenn Sie Befehle ausführen oder eine Region mit dem Befehl `ibmcloud ks region-set` festlegen und den Clusternamen bei der Ausführung von Befehlen verwenden.

<p class="deprecated">Traditionelles Verhalten:</br>Wenn Sie das {{site.data.keyword.containerlong_notm}}-Plug-in Version <code>0.3</code> oder höher verwenden und nur Ressourcen aus einer Region auflisten und damit arbeiten müssen, können Sie mit dem [Befehl](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_init) <code>ibmcloud ks init</code> einen regionalen Endpunkt anstelle des globalen Endpunkts als Ziel verwenden.</br>Wenn Sie die [Umgebungsvariable <code>IKS_BETA_VERSION</code> im {{site.data.keyword.containerlong_notm}}-Plug-in auf <code>0.2</code>](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_beta) setzen, dann erstellen und verwalten Sie Cluster speziell für die Region. Verwenden Sie den Befehl <code>ibmcloud ks region-set</code>, um die Region zu ändern.</p>

```
ibmcloud ks region-get
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

</br>
### Veraltet: `ibmcloud ks region-set`
{: #cs_region-set}

Legt die Region für {{site.data.keyword.containerlong_notm}} fest.
{: shortdesc}

Sie können mit Ressourcen arbeiten, auf die Sie an jedem beliebigen Standort Zugriff haben, selbst wenn Sie durch Ausführen von `ibmcloud ks region-set` eine Region festlegen und die Ressource, mit der Sie arbeiten möchten, sich in einer anderen Region befindet. Wenn Sie Cluster mit demselben Namen in verschiedenen Regionen haben, können Sie entweder die Cluster-ID verwenden, wenn Sie Befehle ausführen oder eine Region mit dem Befehl `ibmcloud ks region-set` festlegen und den Clusternamen bei der Ausführung von Befehlen verwenden.

Wenn Sie die Betaversion `0.2` (traditionell) des {{site.data.keyword.containerlong_notm}}-Plug-ins verwenden, erstellen und verwalten Sie Cluster, die für  die Region spezifisch sind. Sie können sich beispielsweise bei {{site.data.keyword.cloud_notm}} in der Region 'Vereinigte Staaten (Süden)' anmelden und einen Cluster erstellen. Anschließend können Sie `ibmcloud ks region-set eu-central` verwenden, um die Region 'Mitteleuropa' als Ziel festzulegen, und einen weiteren Cluster erstellen. Schließlich können Sie `ibmcloud ks region-set us-south` verwenden, um zur Region 'Vereinigte Staaten (Süden)' zurückzukehren und Ihren Cluster in dieser Region zu verwalten.
{: deprecated}

```
ibmcloud ks region-set --region REGION
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

**Befehlsoptionen**:
<dl>
<dt><code>--region <em>REGION</em></code></dt>
<dd>Geben Sie die Region ein, die Sie als Ziel festlegen möchten. Dieser Wert ist optional. Wenn Sie die Region nicht angeben, können Sie sie aus der Liste in der Ausgabe auswählen.

Eine Liste von verfügbaren Regionen finden Sie unter [Standorte](/docs/containers?topic=containers-regions-and-zones). Alternativ können Sie den [Befehl](#cs_regions) `ibmcloud ks regions` verwenden.</dd></dl>

**Beispiel**:
```
ibmcloud ks region-set --region eu-central
```
{: pre}

</br>
### Veraltet: `ibmcloud ks regions`
{: #cs_regions}

Listet die verfügbaren Regionen auf. Der `Region Name` ist der {{site.data.keyword.containerlong_notm}}-Name und der `Region Alias` ist der allgemeine {{site.data.keyword.cloud_notm}}-Name für die Region.
{: shortdesc}

Regionsspezifische Endpunkte werden nicht mehr verwendet. Verwenden Sie stattdessen den [globalen Endpunkt](/docs/containers?topic=containers-regions-and-zones#endpoint).
{: deprecated}

**Erforderliche Mindestberechtigungen:** Keine

**Beispiel**:
```
ibmcloud ks regions
```
{: pre}

**Ausgabe**:
```
Region Name   Region Alias
ap-north      jp-tok
ap-south      au-syd
eu-central    eu-de
uk-south      eu-gb
us-east       us-east
us-south      us-south
```
{: screen}

</br>
### `ibmcloud ks supported-locations`
{: #cs_supported-locations}

Listet die Standorte auf, die von {{site.data.keyword.containerlong_notm}} unterstützt werden. Weitere Informationen zu den Standorten, die zurückgegeben werden, finden Sie unter [{{site.data.keyword.containerlong_notm}}-Standorte](/docs/containers?topic=containers-regions-and-zones#locations).
{: shortdesc}



```
ibmcloud ks supported-locations
```
{: pre}

**Erforderliche Mindestberechtigungen:** Keine

</br>
### `ibmcloud ks zones`
{: #cs_datacenters}

Liste der verfügbaren Zonen zum Erstellen eines Clusters anzeigen
{: shortdesc}



Wenn Sie die Betaversion `0.2` (traditionell) des {{site.data.keyword.containerlong_notm}}-Plug-ins verwenden, variieren die verfügbaren Zonen abhängig von der Region, bei der Sie angemeldet sind. Um zwischen Regionen zu wechseln, führen Sie den Befehl `ibmcloud ks region-set` aus.
{: deprecated}

```
ibmcloud ks zones [--locations STANDORT] [--region-only] [--json] [-s]
```
{: pre}

**Mindestberechtigungen**: Keine

**Befehlsoptionen**:
<dl>
<dt><code>--locations <em>STANDORT</em></code></dt>
<dd>Filtert Zonen nach einem bestimmten Standort oder nach einer Liste durch Kommas getrennter Standorte. Führen Sie den Befehl <code>ibmcloud ks supported-locations</code> aus, um die unterstützten Standorte anzuzeigen.</dd>

<dt><code>--region-only</code></dt>
<dd>Listet nur Mehrzonencluster in der Region auf, in der Sie angemeldet sind. Dieser Wert ist optional.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks zones --locations ap
```
{: pre}

<br />



## Befehle für Workerknoten
{: worker_node_commands}

### Veraltet: `ibmcloud ks worker-add`
{: #cs_worker_add}

Fügen Sie eigenständige Workerknoten zu einem Cluster hinzu.
{: shortdesc}

Dieser Befehl wird nicht mehr verwendet. Erstellen Sie einen Worker-Pool, indem Sie [`ibmcloud ks worker-pool-create`](#cs_worker_pool_create) ausführen, oder fügen Sie einem vorhandenen Worker-Pool mit dem Befehl [`ibmcloud ks worker-pool-resize`](#cs_worker_pool_resize) Worker hinzu.
{: deprecated}

```
ibmcloud ks worker-add --cluster CLUSTER [--file DATEIPOSITION] [--hardware HARDWARE] --machine-type MASCHINENTYP --workers ANZAHL --private-vlan PRIVATES_VLAN --public-vlan ÖFFENTLICHES_VLAN [--disable-disk-encrypt] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--file <em>DATEIPOSITION</em></code></dt>
<dd>Der Pfad zur YAML-Datei für das Hinzufügen von Workerknoten zum Cluster. Statt zusätzliche Workerknoten mithilfe der in diesem Befehl bereitgestellten Optionen zu definieren, können Sie eine YAML-Datei verwenden. Dieser Wert ist optional.

<p class="note">Wenn Sie dieselbe Option wie im Befehl als Parameter in der YAML-Datei bereitstellen, hat der Wert im Befehl Vorrang vor dem Wert in der YAML. Beispiel: Sie definieren einen Typ in Ihrer YAML-Datei und verwenden die Option <code>--machine-type</code> im Befehl. Der Wert, den Sie in die Befehlsoption eingegeben haben, überschreibt den Wert in der YAML-Datei.</p>

<pre class="codeblock">
<code>name: <em>&lt;clustername_oder_-id&gt;</em>
zone: <em>&lt;zone&gt;</em>
machine-type: <em>&lt;maschinentyp&gt;</em>
private-vlan: <em>&lt;privates_vlan&gt;</em>
public-vlan: <em>&lt;öffentliches_vlan&gt;</em>
hardware: <em>&lt;shared_oder_dedicated&gt;</em>
workerNum: <em>&lt;anzahl_worker&gt;</em>
diskEncryption: <em>false</em></code></pre>

<table>
<caption>Erklärung der Komponenten der YAML-Datei</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Ideensymbol"/> Erklärung der YAML-Dateikomponenten</th>
</thead>
<tbody>
<tr>
<td><code><em>name</em></code></td>
<td>Ersetzen Sie <code><em>&lt;clustername_oder_-id&gt;</em></code> durch den Namen oder die ID des Clusters, in dem Sie Workerknoten hinzufügen möchten.</td>
</tr>
<tr>
<td><code><em>zone</em></code></td>
<td>Ersetzen Sie <code><em>&lt;zone&gt;</em></code> durch die Zone, in der die Workerknoten bereitgestellt werden sollen. Die verfügbaren Zonen sind abhängig von der Region, in der Sie angemeldet sind. Führen Sie den Befehl <code>ibmcloud ks zones</code> aus, um die verfügbaren Zonen aufzuführen.</td>
</tr>
<tr>
<td><code><em>maschinentyp</em></code></td>
<td>Ersetzen Sie <code><em>&lt;maschinentyp&gt;</em></code> durch den Typ bzw. Maschinentyp, auf dem Sie Ihre Workerknoten bereitstellen möchten. Sie können Ihre Workerknoten als virtuelle Maschinen auf gemeinsam genutzter oder dedizierter Hardware oder als physische Maschinen auf Bare-Metal-Systemen bereitstellen. Die Typen der verfügbaren physischen und virtuellen Maschinen variieren je nach der Zone, in der Sie den Cluster bereitstellen. Weitere Informationen finden Sie im Abschnitt zum [Befehl](#cs_machine_types) `ibmcloud ks flavors (machine-types)`. </td>
</tr>
<tr>
<td><code><em>privates_vlan</em></code></td>
<td>Ersetzen Sie <code><em>&lt;privates_vlan&gt;</em></code> durch die ID des privaten VLANs, das Sie für Ihre Workerknoten verwenden möchten. Führen Sie <code>ibmcloud ks vlans --zone <em>&lt;zone&gt;</em></code> aus und suchen Sie nach VLAN-Routern, die mit <code>bcr</code> (Back-End-Router) beginnen, um verfügbare VLANs aufzulisten.</td>
</tr>
<tr>
<td><code>public-vlan</code></td>
<td>Ersetzen Sie <code>&lt;öffentliches_vlan&gt;</code> durch die ID des öffentlichen VLANs, das Sie für Ihre Workerknoten verwenden möchten. Führen Sie <code>ibmcloud ks vlans --zone &lt;zone&gt;</code> aus und suchen Sie nach VLAN-Routern, die mit <code>fcr</code> (Front-End-Router) beginnen, um verfügbare VLANs aufzulisten. <br><strong>Hinweis:</strong> Wenn Workerknoten nur mit einem privaten VLAN eingerichtet werden, müssen Sie die Kommunikation zwischen Workerknoten und Cluster-Master zulassen, indem Sie den [privaten Serviceendpunkt aktivieren](/docs/containers?topic=containers-cs_network_cluster#set-up-private-se) oder eine [Gateway-Einheit konfigurieren](/docs/containers?topic=containers-plan_clusters#workeruser-master).</td>
</tr>
<tr>
<td><code>hardware</code></td>
<td>Für virtuelle Typen: Der Grad an Hardware-Isolation für Ihren Workerknoten. Verwenden Sie `dedicated`, wenn die verfügbaren physischen Ressourcen nur Ihnen zugeordnet werden sollen, oder `shared`, um zuzulassen, dass physische Ressourcen mit anderen IBM Kunden gemeinsam genutzt werden können. Die Standardeinstellung ist `shared`. </td>
</tr>
<tr>
<td><code>anzahl_worker</code></td>
<td>Ersetzen Sie <code><em>&lt;anzahl_worker&gt;</em></code> durch die Anzahl von Workerknoten, die Sie bereitstellen wollen.</td>
</tr>
<tr>
<td><code>diskEncryption: <em>false</em></code></td>
<td>Workerknoten verfügen standardmäßig über eine 256-Bit-AES-Plattenverschlüsselung. [Weitere Informationen finden Sie hier](/docs/containers?topic=containers-security#encrypted_disk). Um die Verschlüsselung zu inaktivieren, schließen Sie diese Option ein und legen Sie den Wert auf <code>false</code> fest.</td></tr>
</tbody></table></p></dd>

<dt><code>--hardware <em>HARDWARE</em></code></dt>
<dd>Der Grad an Hardware-Isolation für Ihren Workerknoten. Verwenden Sie `dedicated`, wenn die verfügbaren physischen Ressourcen nur Ihnen zugeordnet werden sollen, oder `shared`, um zuzulassen, dass physische Ressourcen mit anderen IBM Kunden gemeinsam genutzt werden können. Die Standardeinstellung ist `shared`. Dieser Wert ist optional. Geben Sie für Bare-Metal-Tyen `dedicated` an. </dd>

<dt><code>--machine-type <em>MASCHINENTYP</em></code></dt>
<dd>Wählen Sie für Ihre Workerknoten einen Maschinentyp oder Typ aus. Sie können Ihre Workerknoten als virtuelle Maschinen auf gemeinsam genutzter oder dedizierter Hardware oder als physische Maschinen auf Bare-Metal-Systemen bereitstellen. Die Typen der verfügbaren physischen und virtuellen Maschinen variieren je nach der Zone, in der Sie den Cluster bereitstellen. Weitere Informationen finden Sie in der Dokumentation zum [Befehl](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_machine_types) `ibmcloud ks flavors (machine-types)`. Dieser Wert ist für Standardcluster erforderlich und steht für kostenlose Cluster nicht zur Verfügung.</dd>

<dt><code>--workers <em>ANZAHL</em></code></dt>
<dd>Die durch eine Ganzzahl angegebene Anzahl der Workerknoten, die im Cluster erstellt werden sollen. Der Standardwert ist 1. Dieser Wert ist optional.</dd>

<dt><code>--private-vlan <em>PRIVATES_VLAN</em></code></dt>
<dd>Das private VLAN, das bei der Erstellung des Clusters angegeben wurde. Dieser Wert ist erforderlich. Private VLAN-Router beginnen immer mit <code>bcr</code> (Back-End-Router) und öffentliche VLAN-Router immer mit <code>fcr</code> (Front-End-Router). Wenn Sie einen Cluster erstellen und die öffentlichen und privaten VLANs angeben, muss die Zahlen- und Buchstabenkombination nach diesen Präfixen übereinstimmen. </dd>

<dt><code>--public-vlan <em>ÖFFENTLICHES_VLAN</em></code></dt>
<dd>Das öffentliche VLAN, das bei der Erstellung des Clusters angegeben wurde. Dieser Wert ist optional. Wenn Ihre Workerknoten ausschließlich in einem privaten VLAN bereitgestellt werden sollen, geben Sie keine öffentliche VLAN-ID an. Private VLAN-Router beginnen immer mit <code>bcr</code> (Back-End-Router) und öffentliche VLAN-Router immer mit <code>fcr</code> (Front-End-Router). Wenn Sie einen Cluster erstellen und die öffentlichen und privaten VLANs angeben, muss die Zahlen- und Buchstabenkombination nach diesen Präfixen übereinstimmen. <p class="note">Wenn Workerknoten nur mit einem privaten VLAN eingerichtet werden, müssen Sie die Kommunikation zwischen Workerknoten und Cluster-Master zulassen, indem Sie den [privaten Serviceendpunkt aktivieren](/docs/containers?topic=containers-cs_network_cluster#set-up-private-se) oder eine [Gateway-Einheit konfigurieren](/docs/containers?topic=containers-plan_clusters#workeruser-master).</p></dd>

<dt><code>--disable-disk-encrypt</code></dt>
<dd>Workerknoten verfügen standardmäßig über eine 256-Bit-AES-Plattenverschlüsselung. [Weitere Informationen finden Sie hier](/docs/containers?topic=containers-security#encrypted_disk). Wenn Sie die Verschlüsselung inaktivieren möchten, schließen Sie diese Option ein.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>

</dl>

**Beispiel**:
```
ibmcloud ks worker-add --cluster my_cluster --workers 3 --public-vlan my_public_VLAN_ID --private-vlan my_private_VLAN_ID --machine-type b3c.4x16 --hardware shared
```
{: pre}

</br>
### `ibmcloud ks worker-get`
{: #cs_worker_get}

Zeigt die Details eines Workerknotens an.
{: shortdesc}



```
ibmcloud ks worker-get --cluster CLUSTERNAME_ODER_-ID --worker WORKERKNOTEN-ID [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTERNAME_ODER_-ID</em></code></dt>
<dd>Der Name oder die ID des Workerknotenclusters. Dieser Wert ist optional.</dd>

<dt><code>--worker <em>WORKERKNOTEN-ID</em></code></dt>
<dd>Der Name Ihres Workerknotens. Führen Sie <code>ibmcloud ks workers --cluster <em>CLUSTER</em></code> aus, um die IDs für die Workerknoten in einem Cluster anzuzeigen. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-get --cluster mein_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1
```
{: pre}

**Beispielausgabe**:

  ```
  ID:           kube-dal10-123456789-w1
  State:        normal
  Status:       Ready
  Trust:        disabled
  Private VLAN: 223xxxx
  Public VLAN:  223xxxx
  Private IP:   10.xxx.xx.xxx
  Public IP:    169.xx.xxx.xxx
  Hardware:     shared
  Zone:         dal10
  Version:      1.8.11_1509
  ```
  {: screen}

</br>
### `ibmcloud ks worker-reboot`
{: #cs_worker_reboot}

Führt einen Warmstart eines Workerknotens in einem Cluster durch.
{: shortdesc}



Während des Warmstarts ändert sich der Status Ihres Workerknotens nicht. Sie können z. B. einen Warmstart durchführen, wenn der Status des Workerknotens in der IBM Cloud-Infrastruktur `Powered Off` (ausgeschaltet) lautet und Sie den Workerknoten aktivieren müssen. Ein Warmstart bereinigt zwar die temporären Verzeichnisse, bereinigt jedoch nicht das gesamte Dateisystem und formatiert keine Platten neu. Die IP-Adresse des Workerknotens bleibt nach dem Warmstart unverändert.

Der Warmstart eines Workerknotens kann zu Datenverlust auf dem Workerknoten führen. Verwenden Sie diesen Befehl mit Bedacht und wenn Sie wissen, dass ein Warmstart die Wiederherstellung Ihres Workerknotens unterstützen kann. In allen anderen Fällen sollten Sie stattdessen [Ihren Workerknoten erneut laden](#cs_worker_reload).
{: important}

Stellen Sie, bevor Sie einen Warmstart für Ihren Workerknoten durchführen, sicher, dass die Pods erneut auf anderen Workerknoten geplant werden, um Ausfallzeiten für Ihre App oder Datenverlust auf Ihrem Workerknoten zu vermeiden.

1. Listen Sie die Workerknoten in Ihrem Cluster auf und notieren Sie sich den **Namen** des Workerknotens, den Sie entfernen möchten.
   ```
   kubectl get nodes
   ```
   {: pre}
   Der **Name**, der in diesem Befehl zurückgegeben wird, ist die private IP-Adresse, die Ihrem Workerknoten zugewiesen ist. Weitere Informationen zu Ihrem Workerknoten finden Sie, wenn Sie den Befehl `ibmcloud ks workers --cluster <clustername_oder-id>` ausführen und nach dem Workerknoten mit derselben **privaten IP-Adresse** suchen.

2. Markieren Sie den Workerknoten in einem Prozess, der als Abriegelung oder "Cordoning" bezeichnet wird, als nicht planbar ("unschedulable"). Wenn Sie einen Workerknoten abriegeln, ist er für die künftige Pod-Planung nicht mehr verfügbar. Verwenden Sie den **Namen** des Workerknotens, den Sie im vorherigen Schritt erhalten haben.
   ```
   kubectl cordon <workername>
   ```
   {: pre}

3. Überprüfen Sie, ob die Pod-Planung für Ihren Workerknoten inaktiviert ist
   ```
   kubectl get nodes
   ```
   {: pre}
   Ihr Workerknoten ist für die Pod-Planung inaktiviert, wenn der Status **SchedulingDisabled** angezeigt wird.

4. Pods müssen aus Ihrem Workerknoten entfernt und auf den verbleibenden Workerknoten im Cluster erneut geplant werden.
  ```
  kubectl drain <workername>
  ```
  {: pre}
  Dieser Prozess kann einige Minuten dauern.
5. Führen Sie einen Warmstart für den Workerknoten durch. Verwenden Sie die Worker-ID, die von dem Befehl `ibmcloud ks workers --cluster <clustername_oder_-id>` zurückgegben wird.
  ```
  ibmcloud ks worker-reboot --cluster <clustername_oder_-id> --workers <workername_oder_-id>
  ```
  {: pre}
6. Warten Sie ungefähr 5 Minuten, bevor Sie Ihre Workerknoten für die Pod-Planung zur Verfügung stellen, um sicherzustellen, dass der Warmstart abgeschlossen ist. Während des Warmstarts ändert sich der Status Ihres Workerknotens nicht. Der Warmstart eines Workerknotens ist in der Regel in wenigen Sekunden abgeschlossen.
7. Stellen Sie Ihre Workerknoten für die Pod-Planung zur Verfügung. Verwenden Sie für Ihren Workerknoten den **Namen**, der vom Befehl `kubectl get nodes` zurückgegeben wurde.
  ```
  kubectl uncordon <workername>
  ```
  {: pre}

  </br>

```
ibmcloud ks worker-reboot [-f] [--hard] --cluster CLUSTER --worker WORKER [WORKER] [--skip-master-healthcheck] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-f</code></dt>
<dd>Verwenden Sie diese Option, um den Neustart des Workerknotens ohne Benutzereingabeaufforderungen zu erzwingen. Dieser Wert ist optional.</dd>

<dt><code>--hard</code></dt>
<dd>Geben Sie diese Option an, um einen plötzlichen Neustart eines Workerknotens zu erzwingen, indem Sie die Stromversorgung zum Workerknoten kappen. Verwenden Sie diese Option, wenn der Workerknoten oder die Containerlaufzeit des Workerknotens nicht antwortet. Dieser Wert ist optional.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>Der Name oder die ID einzelner oder mehrerer Workerknoten. Trennen Sie bei einer Auflistung mehrerer Workerknoten die einzelnen Auflistungselemente jeweils durch ein Leerzeichen. Dieser Wert ist erforderlich.</dd>

<dt><code>--skip-master-healthcheck</code></dt>
<dd>Überspringt die Statusprüfung des Masters, bevor die Workerknoten erneut geladen oder gestartet werden.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-reboot --cluster mein_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud ks worker-reload`
{: #cs_worker_reload}

Lädt die Konfigurationen für einen Workerknoten erneut.
{: shortdesc}



Ein erneutes Laden kann sinnvoll sein, wenn Ihr Workerknoten Probleme wie zum Beispiel langsames Laden aufweist oder wenn Ihr Knoten in einem nicht einwandfreien Zustand verharrt. Während des erneuten Ladens wird Ihre Workerknotenmaschine mit dem neuesten Image aktualisiert und die Daten werden gelöscht, wenn sie nicht [außerhalb des Workerknotens gespeichert sind](/docs/containers?topic=containers-storage_planning#persistent_storage_overview). Die öffentliche und die private IP-Adresse des Workerknotens bleiben nach dem erneuten Laden unverändert.


Durch das erneute Laden eines Workerknotens werden Aktualisierungen von Patchversionen auf den Workerknoten angewendet; dies gilt jedoch nicht für Aktualisierungen von Haupt- oder Nebenversionen. Informationen zu den Änderungen von einer Patchversion zur nächsten finden Sie in der Dokumentation zum [Versionsänderungsprotokoll](/docs/containers?topic=containers-changelog#changelog).
{: tip}

Stellen Sie, bevor Sie Ihren Workerknoten erneut laden, sicher, dass die Pods erneut auf anderen Workerknoten geplant werden, um Ausfallzeiten für Ihre App oder Datenverlust auf Ihrem Workerknoten zu vermeiden.

1. Listen Sie die Workerknoten in Ihrem Cluster auf und notieren Sie sich den **Namen** des Workerknotens, den Sie erneut laden möchten.
   ```
   kubectl get nodes
   ```
   Der **Name**, der in diesem Befehl zurückgegeben wird, ist die private IP-Adresse, die Ihrem Workerknoten zugewiesen ist. Weitere Informationen zu Ihrem Workerknoten finden Sie, wenn Sie den Befehl `ibmcloud ks workers --cluster <clustername_oder-id>` ausführen und nach dem Workerknoten mit derselben **privaten IP-Adresse** suchen.
2. Markieren Sie den Workerknoten in einem Prozess, der als Abriegelung oder "Cordoning" bezeichnet wird, als nicht planbar ("unschedulable"). Wenn Sie einen Workerknoten abriegeln, ist er für die künftige Pod-Planung nicht mehr verfügbar. Verwenden Sie den **Namen** des Workerknotens, den Sie im vorherigen Schritt erhalten haben.
   ```
   kubectl cordon <workername>
   ```
   {: pre}

3. Überprüfen Sie, ob die Pod-Planung für Ihren Workerknoten inaktiviert ist
   ```
   kubectl get nodes
   ```
   {: pre}
   Ihr Workerknoten ist für die Pod-Planung inaktiviert, wenn der Status **SchedulingDisabled** angezeigt wird.
 4. Pods müssen aus Ihrem Workerknoten entfernt und auf den verbleibenden Workerknoten im Cluster erneut geplant werden.
    ```
    kubectl drain <workername>
    ```
    {: pre}
    Dieser Prozess kann einige Minuten dauern.
 5. Laden Sie den Workerknoten erneut. Verwenden Sie die Worker-ID, die von dem Befehl `ibmcloud ks workers --cluster <clustername_oder_-id>` zurückgegben wird.
    ```
    ibmcloud ks worker-reload --cluster <clustername_oder_-id> --workers <workername_oder_-id>
    ```
    {: pre}
 6. Warten Sie, bis das erneute Laden abgeschlossen ist.
 7. Stellen Sie Ihre Workerknoten für die Pod-Planung zur Verfügung. Verwenden Sie für Ihren Workerknoten den **Namen**, der vom Befehl `kubectl get nodes` zurückgegeben wurde.
    ```
    kubectl uncordon <workername>
    ```
</br>


```
ibmcloud ks worker-reload --cluster CLUSTER --workers WORKER [WORKER] [--skip-master-healthcheck] [-f] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--worker <em>WORKER</em></code></dt>
<dd>Der Name oder die ID einzelner oder mehrerer Workerknoten. Trennen Sie bei einer Auflistung mehrerer Workerknoten die einzelnen Auflistungselemente jeweils durch ein Leerzeichen. Dieser Wert ist erforderlich.</dd>

<dt><code>--skip-master-healthcheck</code></dt>
<dd>Überspringt die Statusprüfung des Masters, bevor die Workerknoten erneut geladen oder gestartet werden.</dd>

<dt><code>-f</code></dt>
<dd>Verwenden Sie diese Option, um das erneute Laden eines Workerknotens ohne Benutzereingabeaufforderungen zu erzwingen. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-reload --cluster mein_cluster --workers kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>


### `ibmcloud ks worker-rm`
{: #cs_worker_rm}

Entfernt einen oder mehrere Workerknoten von einem Cluster. Wenn Sie einen Workerknoten entfernen, ist Ihr Cluster nicht mehr ausgeglichen. Sie können Ihren Worker-Pool automatisch neu ausgleichen, indem Sie den [Befehl `ibmcloud ks worker-pool-rebalance`](#cs_rebalance) ausführen.
{: shortdesc}



Stellen Sie, bevor Sie Ihren Workerknoten entfernen, sicher, dass die Pods erneut auf anderen Workerknoten geplant werden, um Ausfallzeiten für Ihre App oder Datenverlust auf Ihrem Workerknoten zu vermeiden.
{: tip}

1. Listen Sie die Workerknoten in Ihrem Cluster auf und notieren Sie sich den **Namen** des Workerknotens, den Sie entfernen möchten.
   ```
   kubectl get nodes
   ```
   {: pre}
   Der **Name**, der in diesem Befehl zurückgegeben wird, ist die private IP-Adresse, die Ihrem Workerknoten zugewiesen ist. Weitere Informationen zu Ihrem Workerknoten finden Sie, wenn Sie den Befehl `ibmcloud ks workers --cluster <clustername_oder-id>` ausführen und nach dem Workerknoten mit derselben **privaten IP-Adresse** suchen.
2. Markieren Sie den Workerknoten in einem Prozess, der als Abriegelung oder "Cordoning" bezeichnet wird, als nicht planbar ("unschedulable"). Wenn Sie einen Workerknoten abriegeln, ist er für die künftige Pod-Planung nicht mehr verfügbar. Verwenden Sie den **Namen** des Workerknotens, den Sie im vorherigen Schritt erhalten haben.
   ```
   kubectl cordon <workername>
   ```
   {: pre}

3. Überprüfen Sie, ob die Pod-Planung für Ihren Workerknoten inaktiviert ist
   ```
   kubectl get nodes
   ```
   {: pre}
   Ihr Workerknoten ist für die Pod-Planung inaktiviert, wenn der Status **SchedulingDisabled** angezeigt wird.
4. Pods müssen aus Ihrem Workerknoten entfernt und auf den verbleibenden Workerknoten im Cluster erneut geplant werden.
   ```
   kubectl drain <workername>
   ```
   {: pre}
   Dieser Prozess kann einige Minuten dauern.
5. Entfernen Sie den Workerknoten. Verwenden Sie die Worker-ID, die von dem Befehl `ibmcloud ks workers --cluster <clustername_oder_-id>` zurückgegben wird.
   ```
   ibmcloud ks worker-rm --cluster <clustername_oder_-id> --worker <workername_oder_-id>
   ```
   {: pre}
6. Überprüfen Sie, ob der Workerknoten entfernt wurde.
   ```
   ibmcloud ks workers --cluster <clustername_oder_-id>
   ```
   {: pre}
</br>

```
ibmcloud ks worker-rm [-f] --cluster CLUSTER --workers WORKER[,WORKER] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-f</code></dt>
<dd>Verwenden Sie diese Option, um das Entfernen eines Workerknotens ohne Benutzereingabeaufforderungen zu erzwingen. Dieser Wert ist optional.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>Der Name oder die ID einzelner oder mehrerer Workerknoten. Trennen Sie bei einer Auflistung mehrerer Workerknoten die einzelnen Auflistungselemente jeweils durch ein Leerzeichen. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-rm --cluster mein_cluster --workers kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud ks worker-update`
{: #cs_worker_update}

Aktualisiert Workerknoten, um die neuesten Sicherheitsupdates und Patches auf das Betriebssystem anzuwenden und um die Kubernetes-Version auf die Version des Kubernetes-Master zu aktualisieren. Sie können die Version des Kubernetes-Masters mit dem [Befehl](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_update) `ibmcloud ks cluster-update` aktualisieren. Die IP-Adresse des Workerknotens bleibt nach dem Aktualisieren unverändert.
{: shortdesc}



Durch die Ausführung von `ibmcloud ks worker-update` kann es zu Ausfallzeiten bei Ihren Apps und Services kommen. Während der Aktualisierung wird die Planung aller Pods auf anderen Workerknoten neu erstellt, es wird ein neues Image vom Workerknoten erstellt und die Daten werden gelöscht, wenn sie nicht außerhalb des Pods gespeichert wurden. Um Ausfallzeiten zu vermeiden, sollten Sie [sicherstellen, dass genügend Workerknoten vorhanden sind, um die Workload zu verarbeiten, während die ausgewählten Workerknoten aktualisiert werden](/docs/containers?topic=containers-update#worker_node).
{: important}

Möglicherweise müssen Sie Ihre YAML-Dateien für Bereitstellungen vor der Aktualisierung ändern. Lesen Sie die detaillierten Informationen in diesen [Releaseinformationen](/docs/containers?topic=containers-cs_versions).

```
ibmcloud ks worker-update [-f] --cluster CLUSTER --workers WORKER[,WORKER] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, in dem Sie verfügbare Workerknoten auflisten. Dieser Wert ist erforderlich.</dd>

<dt><code>-f</code></dt>
<dd>Verwenden Sie diese Option, um die Aktualisierung des Masters ohne Benutzereingabeaufforderungen zu erzwingen. Dieser Wert ist optional.</dd>

<dt><code>--workers <em>WORKER</em></code></dt>
<dd>Die ID einzelner oder mehrerer Workerknoten. Trennen Sie bei einer Auflistung mehrerer Workerknoten die einzelnen Auflistungselemente jeweils durch ein Leerzeichen. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-update --cluster mein_cluster --worker kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w1 kube-dal10-cr18a61a63a6a94b658596aa93d087aaa9-w2
```
{: pre}

</br>
### `ibmcloud ks workers`
{: #cs_workers}

Alle Workerknoten in einem Cluster auflisten
{: shortdesc}



```
ibmcloud ks workers --cluster CLUSTER [--worker-pool POOL] [--show-pools] [--show-deleted] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters für die verfügbaren Workerknoten. Dieser Wert ist erforderlich.</dd>

<dt><code>--worker-pool <em>POOL</em></code></dt>
<dd>Zeigt nur die Workerknoten an, die zum Worker-Pool gehören. Führen Sie den Befehl `ibmcloud ks worker-pools --cluster <clustername_oder_-id>` aus, um verfügbare Worker-Pools aufzulisten. Dieser Wert ist optional.</dd>

<dt><code>--show-pools</code></dt>
<dd>Listet den Worker-Pool auf, zu dem jeder Workerknoten gehört. Dieser Wert ist optional.</dd>

<dt><code>--show-deleted</code></dt>
<dd>Zeigt Workerknoten an, die aus dem Cluster gelöscht wurden, und den Grund für das Löschen. Dieser Wert ist optional.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks workers --cluster mein_cluster
```
{: pre}

<br />


## Befehle für Worker-Pools
{: #worker-pool}

Verwenden Sie diese Befehlsgruppe, um Worker-Pools für einen Cluster anzuzeigen und zu ändern.
{: shortdesc}

### `ibmcloud ks worker-pool-create`
{: #cs_worker_pool_create}

Sie können einen Worker-Pool in Ihrem Cluster erstellen. Wenn Sie einen Worker-Pool hinzufügen, wird ihm standardmäßig keine Zone zugeordnet. Sie geben die gewünschte Anzahl von Workern für jede Zone und die Typen für die Worker an. Der Worker-Pool erhält die Standardversionen von Kubernetes. Um das Erstellen der Worker zu beenden, [fügen Sie eine Zone oder Zonen](#cs_zone_add) zu Ihrem Pool hinzu.
{: shortdesc}



```
ibmcloud ks worker-pool-create --name POOLNAME --cluster CLUSTER --machine-type MASCHINENTYP --size-per-zone WORKERS_PRO_ZONE --hardware ISOLATION [--labels BEZEICHNUNGEN] [--disable-disk-encrypt] [-s] [--json]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--name <em>POOLNAME</em></code></dt>
<dd>Der Name, den Sie Ihrem Worker-Pool geben wollen.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--machine-type <em>MASCHINENTYP</em></code></dt>
<dd>Wählen Sie einen Maschinentyp bzw. Typ aus. Sie können Ihre Workerknoten als virtuelle Maschinen auf gemeinsam genutzter oder dedizierter Hardware oder als physische Maschinen auf Bare-Metal-Systemen bereitstellen. Die Typen der verfügbaren physischen und virtuellen Maschinen variieren je nach der Zone, in der Sie den Cluster bereitstellen. Weitere Informationen finden Sie in der Dokumentation zum [Befehl](#cs_machine_types) `ibmcloud ks flavors (machine-types)`. Dieser Wert ist für Standardcluster erforderlich und steht für kostenlose Cluster nicht zur Verfügung.</dd>

<dt><code>--size-per-zone <em>WORKER_PRO_ZONE</em></code></dt>
<dd>Die Anzahl der Worker, die in jeder Zone erstellt werden sollen. Dieser Wert ist erforderlich und muss '1' oder größer sein.</dd>

<dt><code>--hardware <em>ISOLATION</em></code></dt>
<dd>Der Grad an Hardware-Isolation für Ihren Workerknoten. Verwenden Sie `dedicated`, wenn die verfügbaren physischen Ressourcen nur Ihnen zugeordnet werden sollen, oder `shared`, um zuzulassen, dass physische Ressourcen mit anderen IBM Kunden gemeinsam genutzt werden können. Die Standardeinstellung ist `shared`. Geben Sie für Bare-Metal-Tyen `dedicated` an. Dieser Wert ist erforderlich.</dd>

<dt><code>--labels <em>BEZEICHNUNGEN</em></code></dt>
<dd>Die Bezeichnungen, die Sie den Workern im Pool zuweisen möchten. Beispiel: `<key1>=<val1>`,`<key2>=<val2>`</dd>

<dt><code>--disable-disk-encrpyt</code></dt>
<dd>Gibt an, dass die Platte nicht verschlüsselt ist. Der Standardwert ist <code>false</code>.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-pool-create --name my_pool --cluster my_cluster --machine-type b3c.4x16 --size-per-zone 6
```
{: pre}

</br>


### `ibmcloud ks worker-pool-get`
{: #cs_worker_pool_get}

Zeigt die Details eines Worker-Pools an.
{: shortdesc}



```
ibmcloud ks worker-pool-get --worker-pool WORKER-POOL --cluster CLUSTER [-s] [--json]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--worker-pool <em>WORKER-POOL</em></code></dt>
<dd>Der Name des Workerknoten-Pools, für den die Details angezeigt werden sollen. Führen Sie den Befehl `ibmcloud ks worker-pools --cluster <clustername_oder_-id>` aus, um verfügbare Worker-Pools aufzulisten. Dieser Wert ist erforderlich.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, in dem sich der Worker-Pool befindet. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-pool-get --worker-pool pool1 --cluster mein_cluster
```
{: pre}

**Beispielausgabe**:

  ```
  Name:               pool
  ID:                 a1a11b2222222bb3c33c3d4d44d555e5-f6f777g
  State:              active
  Hardware:           shared
  Zones:              dal10,dal12
  Workers per zone:   3
  Machine type:       b3c.4x16.encrypted
  Labels:             -
  Version:            1.13.8_1512
  ```
  {: screen}

</br>
### `ibmcloud ks worker-pool-rebalance`
{: #cs_rebalance}

Gleicht einen Worker-Pool in einem Cluster neu aus, nachdem Sie einen Workerknoten gelöscht haben. Wenn Sie diesen Befehl ausführen, wird Ihrem Worker-Pool mindestens ein neuer Worker hinzugefügt, sodass der Worker-Pool über die von Ihnen angegebene Anzahl Knoten pro Zone verfügt.
{: shortdesc}



```
ibmcloud ks worker-pool-rebalance --cluster CLUSTER --worker-pool WORKER-POOL [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code><em>--cluster CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code><em>--worker-pool WORKER-POOL</em></code></dt>
<dd>Der Worker-Pool, den Sie neu ausgleichen möchten. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-pool-rebalance --cluster mein_cluster --worker-pool mein_pool
```
{: pre}

</br>
### `ibmcloud ks worker-pool-resize`
{: #cs_worker_pool_resize}

Ändert die Größe des Worker-Pools, um die Anzahl der Workerknoten zu erhöhen oder zu verringern, die sich in den einzelnen Zonen des Clusters befinden. Der Worker-Pool muss mindestens einen Workerknoten aufweisen.
{: shortdesc}



```
ibmcloud ks worker-pool-resize --worker-pool WORKER-POOL --cluster CLUSTER --size-per-zone WORKER_PRO_ZONE [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--worker-pool <em>WORKER-POOL</em></code></dt>
<dd>Der Name des Workerknoten-Pools, der aktualisiert werden soll. Dieser Wert ist erforderlich.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den die Größe von Worker-Pools geändert werden soll. Dieser Wert ist erforderlich.</dd>

<dt><code>--size-per-zone <em>WORKER_PRO_ZONE</em></code></dt>
<dd>Die Anzahl der Worker, die in jeder Zone vorhanden sein sollen. Dieser Wert ist erforderlich und muss '1' oder größer sein.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>

</dl>

**Beispiel**:
```
ibmcloud ks worker-pool-resize --cluster mein_cluster --worker-pool mein_pool --size-per-zone 3
```
{: pre}

</br>
### `ibmcloud ks worker-pool-rm`
{: #cs_worker_pool_rm}

Entfernt einen Worker-Pool aus dem Cluster. Alle Workerknoten im Pool werden gelöscht. Die Pods werden beim Löschvorgang neu terminiert. Um Ausfallzeiten zu vermeiden, stellen Sie sicher, dass Sie über genügend Worker zum Ausführen Ihrer Workload verfügen.
{: shortdesc}



```
ibmcloud ks worker-pool-rm --worker-pool WORKER_POOL --cluster CLUSTER [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--worker-pool <em>WORKER-POOL</em></code></dt>
<dd>Der Name des Workerknoten-Pools, der entfernt werden soll. Dieser Wert ist erforderlich.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters, aus dem der Worker-Pool entfernt werden soll. Dieser Wert ist erforderlich.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-pool-rm --cluster mein_cluster --worker-pool pool1
```
{: pre}

</br>
### `ibmcloud ks worker-pools`
{: #cs_worker_pools}

Alle Worker-Pools in einem Cluster auflisten
{: shortdesc}



```
ibmcloud ks worker-pools --cluster CLUSTER [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Anzeigeberechtigter** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--cluster <em>CLUSTERNAME_ODER_-ID</em></code></dt>
<dd>Der Name oder die ID des Clusters, für den Worker-Pools aufgelistet werden sollen. Dieser Wert ist erforderlich.</dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks worker-pools --cluster mein_cluster
```
{: pre}

</br>
### `ibmcloud ks zone-add`
{: #cs_zone_add}

Nachdem Sie einen Cluster oder Worker-Pool erstellt haben, können Sie eine Zone hinzufügen. Wenn Sie eine Zone hinzufügen, werden die Workerknoten der neuen Zone hinzugefügt, damit sie der Anzahl der Worker pro Zone entsprechen, die Sie für den Worker-Pool angegeben haben. Sie können nur dann mehrere Zonen hinzufügen, wenn sich Ihr Cluster in einer Metropole mit mehreren Zonen befindet.
{: shortdesc}



```
ibmcloud ks zone-add --zone ZONE --cluster CLUSTER --worker-pools WORKER-POOL1[,WORKER-POOL2] --private-vlan PRIVATES_VLAN [--public-vlan ÖFFENTLICHES_VLAN] [--private-only] [--json] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Die Zone, die Sie hinzufügen möchten. Es muss sich um eine [für mehrere Zonen geeignete Zone](/docs/containers?topic=containers-regions-and-zones#zones) in der Region des Clusters handeln. Dieser Wert ist erforderlich.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--worker-pool <em>WORKER-POOLS</em></code></dt>
<dd>Eine durch Kommas getrennte Liste der Worker-Pools, zu denen die Zone hinzugefügt wird. Es ist mindestens ein (1) Worker-Pool erforderlich.</dd>

<dt><code>--private-vlan <em>PRIVATES_VLAN</em></code></dt>
<dd><p>Die ID des privaten VLAN. Dieser Wert ist bedingt.</p>
    <p>Wenn Sie über ein privates VLAN in der Zone verfügen, muss dieser Wert mit der privaten VLAN-ID von mindestens einem Workerknoten im Cluster übereinstimmen. Wenn Sie die verfügbaren VLANs anzeigen möchten, führen Sie den Befehl <code>ibmcloud ks cluster-get --cluster &lt;cluster&gt; --showResources</code> aus. Neue Workerknoten werden dem von Ihnen angegebenen VLAN hinzugefügt, die VLANs für alle vorhandenen Workerknoten werden jedoch nicht geändert.</p>
    <p>Wenn Sie in dieser Zone kein privates oder öffentliches VLAN haben, geben Sie diese Option nicht an. Ein privates und ein öffentliches VLAN werden automatisch für Sie erstellt, wenn Sie Ihrem Worker-Pool erstmals eine Zone hinzufügen.</p>
    <p>Wenn Sie über mehrere VLANs für einen Cluster, mehrere Teilnetze in demselben VLAN oder einen Cluster mit mehreren Zonen verfügen, müssen Sie [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) für Ihr Konto in der IBM Cloud-Infrastruktur aktivieren, damit die Workerknoten über das private Netz miteinander kommunizieren können. Zur Aktivierung von VRF [wenden Sie sich an den Ansprechpartner für Ihr Konto der IBM Cloud-Infrastruktur](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Wenn Sie prüfen wollen, ob VRF bereits aktiviert wurde, dann verwenden Sie den Befehl `ibmcloud account show`. Wenn Sie VRF nicht aktivieren können oder wollen, aktivieren Sie [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Um diese Aktion durchführen zu können, müssen Sie über [Infrastrukturberechtigung](/docs/containers?topic=containers-users#infra_access) **Netz > VLAN Spanning im Netz verwalten** verfügen oder Sie können den Kontoeigner bitten, diese zu aktivieren. Zum Prüfen, ob VLAN Spanning bereits aktiviert ist, verwenden Sie den [Befehl](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud ks vlan-spanning-get --region <region>`.</p></dd>

<dt><code>--public-vlan <em>ÖFFENTLICHES_VLAN</em></code></dt>
<dd><p>Die ID des öffentlichen VLANs. Dieser Wert ist erforderlich, wenn Sie Workloads auf den Knoten der Öffentlichkeit zugänglich machen möchten, nachdem Sie den Cluster erstellt haben. Die ID muss mit der öffentlichen VLAN-ID eines oder mehrerer Workerknoten im Cluster für die Zone übereinstimmen. Wenn Sie die verfügbaren VLANs anzeigen möchten, führen Sie den Befehl <code>ibmcloud ks cluster-get --cluster &lt;cluster&gt; --showResources</code> aus. Neue Workerknoten werden dem von Ihnen angegebenen VLAN hinzugefügt, die VLANs für alle vorhandenen Workerknoten werden jedoch nicht geändert.</p>
    <p>Wenn Sie in dieser Zone kein privates oder öffentliches VLAN haben, geben Sie diese Option nicht an. Ein privates und ein öffentliches VLAN werden automatisch für Sie erstellt, wenn Sie Ihrem Worker-Pool erstmals eine Zone hinzufügen.</p>
    <p>Wenn Sie über mehrere VLANs für einen Cluster, mehrere Teilnetze in demselben VLAN oder einen Cluster mit mehreren Zonen verfügen, müssen Sie [VRF (Virtual Router Function)](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) für Ihr Konto in der IBM Cloud-Infrastruktur aktivieren, damit die Workerknoten über das private Netz miteinander kommunizieren können. Zur Aktivierung von VRF [wenden Sie sich an den Ansprechpartner für Ihr Konto der IBM Cloud-Infrastruktur](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#how-you-can-initiate-the-conversion). Wenn Sie prüfen wollen, ob VRF bereits aktiviert wurde, dann verwenden Sie den Befehl `ibmcloud account show`. Wenn Sie VRF nicht aktivieren können oder wollen, aktivieren Sie [VLAN Spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning). Um diese Aktion durchführen zu können, müssen Sie über [Infrastrukturberechtigung](/docs/containers?topic=containers-users#infra_access) **Netz > VLAN Spanning im Netz verwalten** verfügen oder Sie können den Kontoeigner bitten, diese zu aktivieren. Zum Prüfen, ob VLAN Spanning bereits aktiviert ist, verwenden Sie den [Befehl](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_vlan_spanning_get) `ibmcloud ks vlan-spanning-get --region <region>`.</p></dd>

<dt><code>--private-only </code></dt>
<dd>Verwenden Sie diese Option, um zu verhindern, dass ein öffentliches VLAN erstellt wird. Dieser Wert ist nur erforderlich, wenn Sie das Flag `--private-vlan` angeben und das Flag `--public-vlan` nicht einschließen.<p class="note">Wenn Workerknoten nur mit einem privaten VLAN eingerichtet werden, müssen Sie den privaten Serviceendpunkt aktivieren oder eine Gateway-Einheit konfigurieren. Weitere Informationen finden Sie unter [Privaten Cluster und Workerknotenkonfiguration planen](/docs/containers?topic=containers-plan_clusters#private_clusters).</p></dd>

<dt><code>--json</code></dt>
<dd>Druckt die Befehlsausgabe im JSON-Format. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks zone-add --zone dal10 --cluster mein_cluster --worker-pools pool1,pool2,pool3 --private-vlan 2294021
```
{: pre}

</br>


### `ibmcloud ks zone-network-set`
{: #cs_zone_network_set}

**Nur Mehrzonencluster**: Legt die Netzmetadaten für einen Worker-Pool so fest, dass sie ein anderes öffentliches oder privates VLAN als zuvor für die Zone verwenden. Workerknoten, die bereits im Pool erstellt wurden, verwenden weiterhin das vorherige öffentliche oder private VLAN, neue Workerknoten in dem Pool verwenden jedoch die neuen Netzdaten.
{: shortdesc}



```
ibmcloud ks zone-network-set --zone ZONE --cluster CLUSTER --worker-pools WORKER-POOL1[,WORKER-POOL2] --private-vlan PRIVATES_VLAN [--public-vlan ÖFFENTLICHES_VLAN] [--private-only] [-f] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Die Zone, die Sie hinzufügen möchten. Es muss sich um eine [für mehrere Zonen geeignete Zone](/docs/containers?topic=containers-regions-and-zones#zones) in der Region des Clusters handeln. Dieser Wert ist erforderlich.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>--worker-pool <em>WORKER-POOLS</em></code></dt>
<dd>Eine durch Kommas getrennte Liste der Worker-Pools, zu denen die Zone hinzugefügt wird. Es ist mindestens ein (1) Worker-Pool erforderlich.</dd>

<dt><code>--private-vlan <em>PRIVATES_VLAN</em></code></dt>
<dd>Die ID des privaten VLAN. Dieser Wert ist erforderlich, unabhängig davon, ob Sie dasselbe oder ein anderes privates VLAN als dasjenige verwenden möchten, das Sie für Ihre anderen Workerknoten verwendet haben. Neue Workerknoten werden dem von Ihnen angegebenen VLAN hinzugefügt, die VLANs für alle vorhandenen Workerknoten werden jedoch nicht geändert.<p class="note">Die privaten und öffentlichen VLANs müssen kompatibel sein, was sich anhand des ID-Präfix **Router** bestimmen lässt.</p></dd>

<dt><code>--public-vlan <em>ÖFFENTLICHES_VLAN</em></code></dt>
<dd>Die ID des öffentlichen VLANs. Dieser Wert ist nur erforderlich, wenn Sie das öffentliche VLAN für die Zone ändern möchten. Um das öffentliche VLAN zu ändern, müssen Sie immer ein kompatibles privates VLAN angeben. Neue Workerknoten werden dem von Ihnen angegebenen VLAN hinzugefügt, die VLANs für alle vorhandenen Workerknoten werden jedoch nicht geändert.<p class="note">Die privaten und öffentlichen VLANs müssen kompatibel sein, was sich anhand des ID-Präfix **Router** bestimmen lässt.</p></dd>

<dt><code>--private-only </code></dt>
<dd>Optional: Hebt die Festlegung des öffentlichen VLAN auf, sodass die Worker in dieser Zone nur mit einem privaten VLAN verbunden sind.</dd>

<dt><code>-f</code></dt>
<dd>Erzwingt die Ausführung des Befehls ohne Eingabeaufforderungen. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Verwendung**:
<ol><li>Überprüfen Sie die VLANs, die in Ihrem Cluster verfügbar sind. <pre class="pre"><code>ibmcloud ks cluster get --cluster &lt;clustername_oder_-id&gt; --showResources</code></pre><p>Beispielausgabe:</p>
<pre class="screen"><code>Subnet VLANs
VLAN ID   Subnet CIDR         Public   User-managed
229xxxx   169.xx.xxx.xxx/29   true     false
229xxxx   10.xxx.xx.x/29      false    false</code></pre></li>
<li>Prüfen Sie, ob die öffentlichen und privaten VLAN-IDs, die Sie verwenden möchten, kompatibel sind. Um kompatibel zu sein, muss der <strong>Router</strong> dieselbe Pod-ID aufweisen. Private VLAN-Router beginnen immer mit <code>bcr</code> (Back-End-Router) und öffentliche VLAN-Router immer mit <code>fcr</code> (Front-End-Router). Wenn Sie einen Cluster erstellen und die öffentlichen und privaten VLANs angeben, muss die Zahlen- und Buchstabenkombination nach diesen Präfixen übereinstimmen. <pre class="pre"><code>ibmcloud ks vlans --zone &lt;zone&gt;</code></pre><p>Beispielausgabe:</p>
<pre class="screen"><code>ID        Name   Number   Type      Router         Supports Virtual Workers
229xxxx          1234     private   bcr01a.dal12   true
229xxxx          5678     public    fcr01a.dal12   true</code></pre><p>Beachten Sie, dass die Pod-IDs des <strong>Routers</strong> übereinstimmen: `01a` und `01a`. Wenn eine Pod-ID `01a` und die andere Pod-ID `02a` ist, können Sie diese IDs für das öffentliche und private VLAN nicht für Ihren Worker-Pool festlegen.</p></li>
<li>Wenn keine VLANs verfügbar sind, können Sie <a href="/docs/infrastructure/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans">neue VLANs bestellen</a>.</li></ol>

**Beispiel**:
```
ibmcloud ks zone-network-set --zone dal10 --cluster mein_cluster --worker-pools pool1,pool2,pool3 --private-vlan 2294021
```
{: pre}

</br>
### `ibmcloud ks zone-rm`
{: #cs_zone_rm}

**Nur Mehrzonencluster**: Entfernt eine Zone aus allen Worker-Pools in Ihrem Cluster. Alle Workerknoten im Worker-Pool für diese Zone werden gelöscht.
{: shortdesc}



Bevor Sie eine Zone entfernen, stellen Sie sicher, dass genügend Workerknoten in anderen Zonen im Cluster vorhanden sind, damit Ihre Pods neu geplant werden können. Durch die erneute Planung Ihrer Pods können Ausfallzeiten für Ihre App oder Datenverluste auf Ihrem Workerknoten verhindert werden.
{: tip}

```
ibmcloud ks zone-rm --zone ZONE --cluster CLUSTER [-f] [-s]
```
{: pre}

**Erforderliche Mindestberechtigungen:** Plattformrolle **Operator** für {{site.data.keyword.containerlong_notm}}

**Befehlsoptionen**:
<dl>
<dt><code>--zone <em>ZONE</em></code></dt>
<dd>Die Zone, die Sie entfernen möchten. Dieser Wert ist erforderlich.</dd>

<dt><code>--cluster <em>CLUSTER</em></code></dt>
<dd>Der Name oder die ID des Clusters. Dieser Wert ist erforderlich.</dd>

<dt><code>-f</code></dt>
<dd>Erzwingt die Aktualisierung ohne Benutzereingabeaufforderungen. Dieser Wert ist optional.</dd>

<dt><code>-s</code></dt>
<dd>Die Tagesnachricht wird nicht angezeigt oder es werden keine Erinnerungen aktualisiert. Dieser Wert ist optional.</dd>
</dl>

**Beispiel**:
```
ibmcloud ks zone-rm --zone dal10 --cluster mein_cluster
```
{: pre}


