# ML4D paper reviews

This is relevant since climate change disproporitoinately affects the developing world, and the authors specifically focus on the developing world. 

Understanding climate-change driven human migration helps develop resilience.

The authors use Gaussian processes to learn what variables can explain impact of floods and storms. Existing methods assume linear or log-linear relationships. Using various types of data to close the gap in studying internal displacement.

Use GPs as interpretable by using covariance function. Data-limited, high-noise regime, so use Bayesian optimization.

The authors choice of using GPs is well-justified since GPs provide interpretability and are well-suited to a noisy, low-data setting. 

This paper presents a solid implementation and empirical results (analyses of different variables), and they describe their data pipeline thoroughly. They characterize the severity of the disaster using Google Earth Engine; it would be great to discuss how satellite and in situ data may be biased (e.g. overrating or underrating), and steps taken to avoid this concern. Then, if such an algorithm is deployed in different countries, this may inadvertently harm people. 

Review #35
This paper raises pressing questions of ethical concerns asosciated with privacy leakage and discrimination in the domain of using machine learnign for forestry applications. It provides some examples of ethical concerns, such as possible negative consequences of carbon credit ratings and crime prediction. It also touches upon an interesting question of how image data can reveal the economic value of forests.


As a result of advocating for so many broad areas, such as considering that the industry ``consider fairness research``, that are not specifically applicable to forestry, the paper ends up not making a strong statement about any particular one. This paper is too vague and does not develop any unique insights that are particular to forestry. The proposed method of using federated learning is a generic description with no validation, evidence of implementation, etc.
