<div id="top"></div>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->
[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/othneildrew/Best-README-Template">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

  <h3 align="center">Back To Office Optimizer</h3>

  <p align="center">
    An optimization algorithm applied to plan the returns to the office or smartworking days for your team.
    <br />
    ·
    <a href="https://github.com/colibri17/back-to-office/issues">Report Bug</a>
    ·
    <a href="https://github.com/colibri17/back-to-office/issues">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project

[![Product Name Screen Shot][product-screenshot]](https://example.com)

This project aims to provide a tool to all managers for better planning the presence of the resources to the office 
or the scheduling of smartworking days.

This planning can be really complicated to perform for humans. Especially if 
there are many constraints to take into account (e.g. return preferences, workstations, maximum 
room capacities and so on), choosing the best configuration can be really hard. Furthermore, 
there are generally no guarantees that the identified solution is the optimal one.

In this regards, an optimization algorithm can help. It can take 
into account different factors, define hard constraints to prevent specified configurations,
and allow to mathematically be sure that the proposed solution is the optimal one.


<p align="right">(<a href="#top">back to top</a>)</p>

### How it works
To optimize the planning, an integer optimization algorithm is used. The optimization model is composed by three main objects:
1. _The decision variables_  
Each decision variable is a binary variable $x_{ij} \in {0,1}$, which represents whether the resource $i$ on day $j$ 
comes back to the office. The number of resources and the number of days to consider can be both
selected within the code.   
Along with these variables, we defined some non-linear decision variables that are obtained as the product of two or more binary variables and
that are used within the code to express terms in the objective functions or in the constraints. 
2. _The objective function_  
The objective function is composed by different terms.
   1. _consecutive days_ - For a resource is easier to come back on consecutive week days, so whenever this occurs the objective function is increased by 1
   2. _same team_ - For a team working together it is better to come back on the same days, so whenever this occurs the objective function is increased. 
   More precisely, if 2 team members come back on the same day the objective function is increased by 1. If 3 team members come back on the same day the objective function is increased by 2, and so on.
   3. _Target presence_ - Every resource should comes back a minimum number of days, encouraging some equity in the returns to the office. So, whenever a resource
   does not reach the mean presence of 2 days a week on the planning period, a penalty equal to the number of missing days is added to the objective function.
   4. _Single returns_ - Return to the office should be encouraged, so the objective function is increased of 1 for each return.

These 4 terms can be weigthed according to personal preferences. Within the code, they all have the same weight. 

3. _The constraints_
There are different types of constraints in the algorithm. Each type is derived from a supposed contingency which is not general and can be customized.
   1. _maximum and minimum number of resources_ - There is a maximum and minimum number of resources which can return to the office each day. The optimization
   algorithm prevents from finding solutions which exceed this maximum number or are below the minimum number. 
   2. _preference days_ - The resources are allowed to choose what are the days to come back and what are the days to not come back. The optimization
   algorithm finds solutions which agree with these preferences.
   3. _linearization constraints_ - Since we want the problem to be linear, non-linear variables are linearized by introducing some extra constraints. 
   This allows to use a linear optimizer making the problem easier to solve optimally.  

As the terms in the objective functions, the constraint types can be customized according to the user preferences and needs. For example,
you might want to remove the preference day constraints, or add some more. Also, notice that according to the needs some terms added to the objective function
might become constraints and vice versa.

<p align="right">(<a href="#top">back to top</a>)</p>

### Built With

This section list any major frameworks/libraries used to bootstrap the project:

* [Python](https://www.python.org/)
* [PuLP](https://coin-or.github.io/pulp/)
* [Pandas](https://vuejs.org/)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

To get a local copy up and running follow these simple example steps.

### Prerequisites

You have to install Python on your system. On Ubuntu 16.10 or newer, this can be done:
  ```sh
  sudo apt-get update
  sudo apt-get install python3
  ```

### Installation

1. Clone the repo
   ```sh
   https://github.com/colibri17/back-to-office
   ```
2. Install `Pandas` and `Pulp` libraries using `pip` 
   ```sh
   pip install -u pandas pulp 
   ```

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Usage
All the code is contained in the notebook `optimizazion.ipynb` 
Use this space to show useful examples of how a project can be used. Additional screenshots, code examples and demos work well in this space. You may also link to more resources.

_For more examples, please refer to the [Documentation](https://example.com)_

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ROADMAP -->
## Roadmap

- [x] Add Changelog
- [x] Add back to top links
- [] Add Additional Templates w/ Examples
- [] Add "components" document to easily copy & paste sections of the readme
- [] Multi-language Support
    - [] Chinese
    - [] Spanish

See the [open issues](https://github.com/othneildrew/Best-README-Template/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Your Name - [@your_twitter](https://twitter.com/your_username) - email@example.com

Project Link: [https://github.com/your_username/repo_name](https://github.com/your_username/repo_name)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

Use this space to list resources you find helpful and would like to give credit to. I've included a few of my favorites to kick things off!

* [Choose an Open Source License](https://choosealicense.com)
* [GitHub Emoji Cheat Sheet](https://www.webpagefx.com/tools/emoji-cheat-sheet)
* [Malven's Flexbox Cheatsheet](https://flexbox.malven.co/)
* [Malven's Grid Cheatsheet](https://grid.malven.co/)
* [Img Shields](https://shields.io)
* [GitHub Pages](https://pages.github.com)
* [Font Awesome](https://fontawesome.com)
* [React Icons](https://react-icons.github.io/react-icons/search)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/othneildrew/Best-README-Template/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/othneildrew/Best-README-Template/network/members
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/othneildrew/Best-README-Template/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/Best-README-Template.svg?style=for-the-badge
[issues-url]: https://github.com/othneildrew/Best-README-Template/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/othneildrew/Best-README-Template/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/othneildrew
[product-screenshot]: images/screenshot.png
