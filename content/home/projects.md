+++
# Accomplishments widget.
widget = "accomplishments"  # See https://sourcethemes.com/academic/docs/page-builder/
headless = true  # This file represents a page section.
active = true  # Activate this widget? true/false
weight = 30  # Order that this section will appear.

title = "Selected Projects"
subtitle = ""

# Date format
#   Refer to https://sourcethemes.com/academic/docs/customization/#date-format
date_format = "Jan 2006"

# Accomplishments.
#   Add/remove as many `[[item]]` blocks below as you like.
#   `title`, `organization` and `date_start` are the required parameters.
#   Leave other parameters empty if not required.
#   Begin/end multi-line descriptions with 3 quotes `"""`.

[[item]]
  organization = "COMP524"
  organization_url = ""
  title = "miniLisp Interpreter"
  date_start = "2021-01-20"
  date_end = "2021-04-02"
  description = """
  * Implemented an environment-passing, OOP interpreter for a lisp-style language from scratch in Racket
  *	Constructed the recursive descent parser based on homoiconicity of Racket and built the lexer using regular expression
  *	Developed lexical scope, procedure, instantiation, inheritance, polymorphism, etc by passing and mutating environment
  """

[[item]]
  organization = "COMP431"
  organization_url = ""
  title = "FTP Client/Server"
  date_start = "2021-01-15"
  date_end = "2021-03-07"
  description = """
  *	Implemented a FTP Client/Server System that supports login, file transfer in Python
  *	Developed common commands (USER, PASS, SYST, TYPE, PORT, RETR, QUIT) and ensured server’s robustness
  *	Achieved C/S communication with TCP socket and maximized client’s fault-tolerance
  """

[[item]]
  organization = "COMP426"
  organization_url = ""
  title = "ApparelUNC"
  date_start = "2020-09-10"
  date_end = "2020-11-27"
  description = """
  *	Designed and implemented a [webapp](https://apparelunc.herokuapp.com/) for helping UNC fans choosing the best UNC outfit using the MERN stack
  *	Constructed database with MongoDB, developed interfaces for CRUD functions in Express, and delopyed the app on Heroku
  *	Designed and improved UI with Bootstrap and used reCAPTCHA to protect the website
  *	Managed the project using SCRUM in a team of 3 and wrote detailed documentation
  """

[[item]]
  organization = "Personal Project"
  organization_url = ""
  title = "Mock MOOC"
  date_start = "2020-07-26"
  date_end = "2020-10-01"
  description = """
  * Developing an online video course platform using **SpringCloud**, **Vue CLI**, **MyBatis**
  * Developed an admin website enables the user to perform CRUD operations on databases
  * Used **FreeMarker** template engine generating codes for service, controller, dto, and vue in 2 minutes
  """

[[item]]
  organization = "STOR 565"
  organization_url = ""
  title = "Insight into NBA Winning Rate"
  date_start = "2020-04-19"
  description = """
  * Applied Gradient Boosting, LASSO, PCA to predict, classify winning percentage of NBA teams in **R**
  * Achieved a 93%+ classifcation accuracy and wrote a 12-page report with two other teammates
  """


[[item]]
  title = "Amazon Customer Reviews Analysis"
  organization = "The Interdisciplinary Contest in Modeling"
  certificate_url = "files/MCM2020_Meritorious_Winner.pdf"
  date_start = "2020-03-01"
  description = """
  Meritorious Winner (top 7%)
  *	Analyzed patterns of Amzon Customer Reviews in **R** and prepared a 19-page report with two teammates
  *	Contributed codes and analysis for sentiment analysis, PCA, EDA, visualization, and Ordinal LogitReg
  """


[[item]]
  organization = "COMP 401 Hackathon"
  organization_url = ""
  title = "Keep My Professor Dry"
  date_start = "2019-11-19"
  description = """
  Best Hack for Water Gun Racing Game
  * Used **Java** Swing to create a challenging water gun racing-like game by randomization and punishment for shooting mistakes
  * Collaborated with 2 teammates using **Git** for version control
  """
+++
