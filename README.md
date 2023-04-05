# Covid-19_firstInsightsbycontinent
Working on how greater Continents are affected by Covid-19  

1. Used Excel To clean data
2. Used SQL to Segregate Date needed
3. Used Tableau For visualization
                 ------------------------------------------------------------
		  -- Percent OF population Infected by date and Location
		 ------------------------------------------------------------
  --table 4
  Select Location, Population ,date , max(total_cases) as highestInfectionCount , Max((total_cases/population))*100 as percentofpopulationInfected 
  From portfolioProject..Covid_Deaths
  --where location like "%india%"
  Group by location, population , date
  order by percentofpopulationInfected desc


                -------------------------------------------------------------
                --Percent of Population Infected by Location alone
		-------------------------------------------------------------
  
  
  --table 3 
   Select Location, Population  , max(total_cases) as highestInfectionCount , Max((total_cases/population))*100 as percentofpopulationInfected 
  From portfolioProject..Covid_Deaths
  --where location like "%india%"
  Group by location, population 
  order by percentofpopulationInfected desc

                ---------------------------------------------------------------
                --showing the highest death rate by continent
	        ---------------------------------------------------------------
  
  --Table 2        
  
  
SELECT 
  continent, 
  Max(
    Cast(total_deaths as int)
  ) as totalDeathCount 
FROM 
  [portfolioProject].[dbo].[Covid_Deaths] 
where 
  continent is not null 
  --Where location like '%India%'
Group By 
  continent 
Order by 
 totalDeathCount desc;

                 ----------------------------------------------------------
                                   --global numbers
                               --Total around the world
	         --------------------------------------------------------

--Table 1
SELECT 
  sum(new_cases) as TotalCases, 
  SUM(new_deaths) as TotalDeaths, 
  Sum(new_deaths)/ Sum (new_cases)* 100 as deathPercent 
FROM 
  [portfolioProject].[dbo].[Covid_Deaths] 
  --Where location like '%India%'
where 
  continent is not null 
   --Group by date
Order by 
  1, 
  2;
