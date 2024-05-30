# Sustainable-Agriculture-Practices-Recommender
This is a crop recommendation system utilizing a bandit algorithm framework to optimize agricultural outputs. By leveraging multi-armed bandit algorithms, the system dynamically adapts to varying environmental conditions and historical crop performance data to recommend the most suitable crop types for specific plots of land


<!--   <ol>
    <li>
      <a href="#about-the-project">About AtyaNidan</a>
      <ul>
        <li><a href="#project-status">Project Status</a></li>
      </ul>
    </li>
    <li>
      <a href="#get-started">Get Started</a>
      <ul>
        <li><a href="#1-build-and-setup">1. Build and Setup</a></li>
        <li><a href="#2-run-the-application">2. Run the Application</a></li>
        <li><a href="#3-individual-server-startup">3. Individual Server Startup</a></li>
      </ul>
    </li>
    <li><a href="#logo">App Logo</a></li> 
    <li><a href="#Figma">Figma</a></li>
    <li><a href="#ScreenShots">Screenshots</a></li> 
  </ol> -->
<!-- </details> -->


## 🔎 Data Collection

Dataset was taken from kaggle (Crop Recommendation Dataset - ATHARVA INGLE). It consisted of following Data fields: N - ratio of Nitrogen content in soil, P - ratio of Phosphorous content in soil, K - ratio of Potassium content in soil, temperature - temperature in degree Celsius, humidity - relative humidity in ph - ph value of the soil, rainfall - rainfall in mm. For each unique crops there were 100 corresponding rows and there were only 22 unique rows, so we decided to generate more unique crops and compress data into single row.

### Data Generation

We had 22 crops in our dataset, to generate more crops we first found correlation between columns. Now to make cohorts we found a threshold using IQR (0.29) and noticed that out data 2 cohorts.

**Cohort 1:** K-mean, P-mean

**Cohort 2:** humidity-mean, temperature-mean

Now we have taken mean of min and max columns of each crop and made entry for it. Then we normalized each values in scale of -1 to 1. Categorical column ’label’ was converted to numerical using One hot encoding. Finally we have made 2 datasets one for local crops and one for the crops that are imported in India. This division helps us promote agriculture of exotic crops which further down the line reduced the import rate. 

<p align="right" style="font-size: 14px; color: #555; margin-top: 20px;">
    <a href="#readme-top" style="text-decoration: none; color: #007bff; font-weight: bold;">
        ↑ Back to Top ↑
    </a>
</p>

## 🐙 Multi-arm Bandit

The crops recommended from content based are passed on to MAB, where each crop is a arm and algorithm picks the most suitable arm.
### Epsilon Greedy: 
Epsilon-greedy is an exploration- exploitation strategy for decision making. It balances choosing the known best option (exploitation) with exploring random options (exploration) to potentially discover better choices. With a small probability (epsilon), the algorithm takes a ran- dom action, helping it escape local optima and find potentially better solutions. We have fixed value of epsilon to be 0.3.
The application simplifies the process of recording diagnoses using ICD10 codes, making it easier for doctors to prescribe the appropriate treatment and follow-ups. It's equipped with features to help health workers manage their schedules, receive alerts for upcoming follow-ups, and ensure no patient is left behind, even in areas with unreliable internet thanks to its offline capabilities.

<p align="right" style="font-size: 14px; color: #555; margin-top: 20px;">
    <a href="#readme-top" style="text-decoration: none; color: #007bff; font-weight: bold;">
        ↑ Back to Top ↑
    </a>
</p>

### Thompsons Sampling: 
Thompson Sampling tackles the multi-armed bandit problem by balancing exploration and exploitation. It maintains probability distributions for each option’s reward. It then samples from these distributions to choose an option, favoring those with potentially higher rewards (exploration). As it gathers data, the distributions update, focusing on options that consistently deliver good rewards (exploitation). The value of alpha and beta are set to 1 initially for this project. It is a Bayesian approach to the multi-armed bandit problem. Instead of directly keeping track of average rewards, it models belief about each crop’s reward with a probability distribution.

**Sample:** For each crop, it draws a random sample from its reward distribution.

**Select:** It chooses the crop with the highest sampled reward.

**Update:** It updates the reward distribution based on the feedback received.

<p align="right" style="font-size: 14px; color: #555; margin-top: 20px;">
    <a href="#readme-top" style="text-decoration: none; color: #007bff; font-weight: bold;">
        ↑ Back to Top ↑
    </a>
</p>

### Upper Confidence Bound

Upper Confidence Bound (UCB) tackles the challenge of balancing established user preferences with the potential for discovering hidden gems. It achieves this by assigning a score to each item. This score combines an item’s historical value (like purchase rate) with a bonus that encourages exploration of less-recommended items. As user interactions accumulate, UCB refines its scores, favoring items that consistently gener- ate positive responses. This approach prevents the system from getting stuck on popular but potentially sub-optimal choices, promoting exploration and potentially leading to the discovery of new favorites for users.
UCB offers a deterministic approach, meaning it calculates a single score for each item based on a clear formula. This allows for easier analysis and control of the exploration- exploitation balance. Thompson Sampling, on the other hand, relies on random sampling from probability distributions, introducing an element of chance in the selection process.

<p align="right" style="font-size: 14px; color: #555; margin-top: 20px;">
    <a href="#readme-top" style="text-decoration: none; color: #007bff; font-weight: bold;">
        ↑ Back to Top ↑
    </a>
</p>

## 😢 Regret analysis

or this project we have assumed farmers ratings to be Gaussian distributed. So, for every recommended crop we have added a assumed mean so that we can have an optimal crop for the soil to calculate regret from in ou case Sababul has the highest mean rating so out of the 5 crops regret will be calculated compared to Sababul. Hence, Sababul should have least regret out of 5.

## 📸 Output Screenshots

#### Epsilon Greedy

<img width="1023" alt="Screenshot 2024-05-30 at 8 10 46 PM" src="https://github.com/nisharathod231/Sustainable-Agriculture-Practices-Recommender/assets/163638504/d2b50455-a0ff-4e32-961f-f37381cb9e72">

#### Thompsons Sampling

<img width="1024" alt="Screenshot 2024-05-30 at 8 11 16 PM" src="https://github.com/nisharathod231/Sustainable-Agriculture-Practices-Recommender/assets/163638504/3a7d3ff5-b99d-4c29-8d64-59d1660eaf36">

#### Linear UCB

<img width="1024" alt="Screenshot 2024-05-30 at 8 12 15 PM" src="https://github.com/nisharathod231/Sustainable-Agriculture-Practices-Recommender/assets/163638504/3e58aeec-4d71-4b67-883b-25eda5a098d0">


<p align="right" style="font-size: 14px; color: #555; margin-top: 20px;">
    <a href="#readme-top" style="text-decoration: none; color: #007bff; font-weight: bold;">
        ↑ Back to Top ↑
    </a>
</p>

[contributors-shield]: https://img.shields.io/github/contributors/opendevin/opendevin?style=for-the-badge
[contributors-url]: https://github.com/OpenDevin/OpenDevin/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/opendevin/opendevin?style=for-the-badge
[forks-url]: https://github.com/OpenDevin/OpenDevin/network/members
[stars-shield]: https://img.shields.io/github/stars/opendevin/opendevin?style=for-the-badge
[stars-url]: https://github.com/OpenDevin/OpenDevin/stargazers
[issues-shield]: https://img.shields.io/github/issues/opendevin/opendevin?style=for-the-badge
[issues-url]: https://github.com/OpenDevin/OpenDevin/issues
[license-shield]: https://img.shields.io/github/license/opendevin/opendevin?style=for-the-badge
[license-url]: https://github.com/OpenDevin/OpenDevin/blob/main/LICENSE
