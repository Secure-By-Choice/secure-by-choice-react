Secure By Choice have decided to fork the RE&CT framework since it has not been updated for a long long time now and it needs to live on.

Atomic Threat Coverage did an amazing job with the original framework.

Secure By Choice aims to continue their legacy and make RE&CT 2.0 a little more simple and more maintainable by stripping down the framework back to basics.

![alt text](https://github.com/Secure-By-Choice/logo/blob/main/SecureByChoiceWhiteLogo.png)

# RE&CT 2.0

The project represents the following:

1. A [framework](https://atc-project.github.io/atc-react/) — knowledge base of actionable Incident Response techniques
2. A community-driven [collection](docs/Response_Playbooks) of Security Incident Response Playbooks

## RE&CT 2.0 Framework

RE&CT 2.0 Framework is designed for accumulating, describing and classification actionable Incident Response techniques. 

RE&CT's philosophy is based on the [MITRE's ATT&CK](https://attack.mitre.org/) framework.  
The columns represent [Response Stages](https://atc-project.github.io/atc-react/responsestages/).  
The cells repsresent [Response Actions](#response-action).  

![](docs/images/react_navigator_export_v5.svg)
<p align="center">(Image generated by <a href="https://atc-project.github.io/react-navigator/">RE&CT Navigator)</a></p>

The main use cases:

- Prioritization of Incident Response capabilities development, including skills development, technical measures acquisition/deployment, internal procedures development, etc
- Gap analysis — determine "coverage" of existing Incident Response capabilities 

### Response Action

Response Action is a description of a specific atomic procedure/task that has to be executed during the Incident Response. It is an initial entity that is used to construct Response Playbooks.  

Here is an example of Response Action:

<details>
  <summary>Initial YAML file (click to expand)</summary>
  <img src="docs/images/ra_yaml_v6.png" />
</details>

- Automatically created [Markdown file](docs/Response_Actions/RA_2202_collect_email_message.md)
- Automatically created [mkdocs web page](https://atc-project.github.io/atc-react/Response_Actions/RA_2202_collect_email_message/)
- Automatically created [Confluence page](https://atomicthreatcoverage.atlassian.net/wiki/spaces/REACT/pages/755435640/RA2202+Collect+email+message)

Each Response Action mapped to a specific [Response Stage](https://atc-project.github.io/atc-react/responsestages/).  

The first digit of the Response Action ID reflects a Stage it belongs to:

- **1**: Preparation
- **2**: Identification
- **3**: Containment
- **4**: Eradication
- **5**: Recovery
- **6**: Lessons Learned

The second digit of the Response Action ID reflects a Category it belongs to:

- **0**: General
- **1**: Network
- **2**: Email
- **3**: File
- **4**: Process
- **5**: Configuration
- **6**: Identity

This way, using Response Action ID, you can see the Stage and Category it belongs to.  
For example, [RA**22**02: Collect an email message](docs/Response_Actions/RA_2202_collect_email_message.md) is related to Stage **2** (Identification) and Category **2** (Email).  

The categorization aims to improve Incident Response process maturity assessment and roadmap development.  

### Response Playbook

Response Playbook is an Incident Response plan, that represents a complete list of procedures/tasks (Response Actions) that has to be executed to respond to a specific threat with optional mapping to the [MITRE's ATT&CK](https://attack.mitre.org/) or [Misinfosec's  AMITT](https://github.com/misinfosecproject/amitt_framework) frameworks.

Here is an example of Response Playbook:

<details>
  <summary>Initial YAML file (click to expand)</summary>
  <img src="docs/images/rp_yaml_v6.png" />
</details>

- Automatically created [Markdown file](docs/Response_Playbooks/RP_0001_phishing_email.md)
- Automatically created [mkdocs web page](https://atc-project.github.io/atc-react/Response_Playbooks/RP_0001_phishing_email/)
- Automatically created [Confluence page](https://atomicthreatcoverage.atlassian.net/wiki/spaces/REACT/pages/755469546/RP0001+Phishing+email)

Response Playbook could include a description of the workflow, specific conditions/requirements, details on the order of Response Actions execution, or any other relevant information.

### TheHive Case Templates

TheHive Case Templates are built on top of the Response Playbooks. Each task in a Case Template is a Response Action (with full description). 

Here is the example of an imported TheHive Case Template:

<details>
  <summary>Imported TheHive Case Template, made on top of a Response Playbook (click to expand)</summary>
  <img src="docs/images/thehive_case_template_v1.png" />
</details>

<details>
  <summary>One of the Tasks in TheHive Case, made on top of a Response Action (click to expand)</summary>
  <img src="docs/images/thehive_case_task_v1.png" />
</details>

TheHive Case Templates could be found in `docs/thehive_templates` directory and could be imported to TheHive via its web interface.

## Data source of the ATC framework

ATC RE&CT project plays a role of data source for the [Atomic Threat Coverage](https://github.com/atc-project/atomic-threat-coverage) framework, that uses it to generate Markdown and Confluence knowledge bases, ATT&CK Navigator layers, Elasticsearch indexes and [other](https://github.com/atc-project/atomic-threat-coverage#how-it-works) analytics. 

Originally analytics related to Incident Response were part of the ATC, but we decided to move it into a separate project to make it easier to maintain and provide an option for integration with other projects in this area. 

## Usage

1. Make sure you are compliant with the [requirements](#requirements)

2. Create configuration file by copying configuration file template `scripts/config.default.yml` to `config.yml` (root of the project). Modify it, following the guideline in the configuration file template.

3. Modify existing `.yml` files, or develop your own analytics using the templates of [Response Actions](response_actions/respose_action.yml.template) or [Response Playbooks](response_playbooks/respose_playbook.yml.template). They should be stored in the directories according to their type.

4. When `.yml` files are ready, convert them to `.md` documents, import them into Confluence, generate TheHive templates and [RE&CT Navigator](https://github.com/atc-project/react-navigator) layer using the following commands:
    ```
    python3 main.py --markdown --auto --init
    python3 main.py --confluence --auto --init
    python3 main.py --thehive
    python3 main.py -NAV
    ```
    You will find the outcome in the `docs` directory and Confluence pages (according to the configuration). Also, the RE&CT Navigator layer could be opened only in the [customized application](https://github.com/atc-project/react-navigator).

5. Generate your own (private) website with your analytics, using [mkdocs](https://www.mkdocs.org/):
    ```
    python3 main.py -MK         # automatic mkdocs config (navigation) generation
    python3 -m mkdocs build
    ```
    The website will be stored in the `site` directory.  You can preview it with the following command:
    ```
    python3 -m mkdocs serve
    ```

### Requirements

- Python 3.7
- [PyYAML](https://pypi.org/project/PyYAML/), [mkdocs](https://pypi.org/project/mkdocs/), [jinja2](https://pypi.org/project/Jinja2/) and [stix2](https://pypi.org/project/stix2/) (optionally)  Python libraries. They could be installed with the following command:
    ```
    python3 -m pip install -r requirements.txt
    ```

## Contacts

- Folow us on [Twitter](https://twitter.com/atc_project) for updates
- Join discussions in [Slack](https://join.slack.com/t/atomicthreatcoverage/shared_invite/zt-6ropl01z-wIdiq3M0AEZPj_HiKfbiBg) or [Telegram](https://t.me/atomic_threat_coverage) 

## Contributors

- Timur Zinniatullin, [@zinint](https://twitter.com/zinint)  
- Daniil Svetlov, [@Mr_4nders0n](https://twitter.com/Mr_4nders0n)  
- Andreas Hunkeler, [@Karneades](https://github.com/Karneades)
- Patrick Abraham, [@pjabes](https://github.com/pjabes)
- Lucas Berezy, [@lberezy](https://github.com/lberezy)
- Efe Erdur, [@efeerdur](https://github.com/efeerdur)
- Alejandro Ortuno, [@aomanzanera](https://twitter.com/aomanzanera)  
- [@d3anp](https://github.com/d3anp)  
- Christoph Bott, [@xofolowski](https://github.com/xofolowski)  

Would you like to become one? You are very welcome! Our [CONTRIBUTING](CONTRIBUTING.md) guideline is a good starting point.
## License

See the [LICENSE](LICENSE) file.
