#HRANA_Report_IranMasscre

This Project Looks into # Parisa_Babaali, NIAC's New York Chapter lead, and her claims about HRNA report of #IranMassacre 

Following Iranian Government's Massacre in Januray 2026, HRANA, an reknown independent human rights organisation has issued a detailed report called , Crimson Winter, The report is available here: (https://www.en-hrana.org/the-crimson-winter-a-50-day-record-of-irans-2025-2026-nationwide-protests/). According to HRANA, this report includes an Appendix of over 4000 people killed by Iranian government officals in that period.

Parisa Babaali, is a senior AI engineer at IBM and a chapter leader of NIAC NY (these are publc info about her, according to Niac website https://niacouncil.org/staff/parisa-babaali/). She has made an Instagram video (https://www.instagram.com/pbabaali/) where she claims she has reviewed this Appendix, and "there are 400 to 500 duplicate names in this report", thereby making a claim of over 400 to 500 people who HRANA has listed don't exist and are duplicates.

We have respectfully asked Ms Babaali to release her analysis via X (former twitter) and Instagram to which she has not reponded.

This Repo, hence, verifies her claims, via an openly available approach and leaves this approach and data for others to cross-examin as well. 

While we undestand that humanitarian organisations may have incomplete info at times or make mistakes in their reported data, we belive "Iranian Lives Matter" like any othet nation's and so, no one should make random claims and assumptions about reports of Irnian people killed and their evidnece, without being able to substanciate their claims.

Our question is simple, are there 400 to 500 duplicate names in this report", or is Parisa Babaali falsifying in her claim?

Also, while HRANA historically makes great efforts to report based on evidence, mistakes or incomplete or duplicated info may happen in documanting crimes of Iranian government, specially and sadly in this magnitude. Hence the other goal of this work is to help HRANA corretc any such findings in their report.

Method and results lsited below:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Downlod HRANA Report
https://www.en-hrana.org/the-crimson-winter-a-50-day-record-of-irans-2025-2026-nationwide-protests/

🔹 Step 1 — Convert source files to PDF

Goal: Standardize format for consistent parsing

Take original files (DOCX / mixed formats)
Convert to PDF using: Adobe Acrobat
Microsoft Word → Save as PDF

✅ Output:

/data/raw/crimson_winter_full.pdf
🔹 🔹 Step 2 — Extract Appendix sections

Goal: Isolate structured victim lists

Open the full report PDF
Identify appendix sections:
Deceased Children
Deceased Adults
Non-protesting civilians
Export each section separately:
Save as PDF or DOCX

✅ Output:

/data/raw/appendix_children.docx
/data/raw/appendix_adults.docx
/data/raw/appendix_non_protesting.docx

🔹 🔹 Step 3 — Prepare structured extraction prompt (We used ChatGPT, but this can be done with othet programing skills)

Goal: Convert semi-structured text → structured table

🔹 For ChatGPT Use the following  prompt template for any of the top files (e.g appendix_adults.docx):

Read this document and convert numbered paragraphs into an Excel table.

Each row must be split into the following columns:

1. ID → number before "-"
2. Name → text between "-" and ":"
3. City of Death → value after "City of Death:"
4. Province → value after "Province:"
5. Date of Death → value after "Date of Death:"
6. First Source → value after "First Source:"
7. Status → value after "HRANA Verification Status:"

Example:
"234 - Meysam Bijani Zarei: City of Death: Shahriar – Province: Tehran – Date of Death: Unknown – First Source: X – HRANA Verification Status: Confirmed"

→
ID: 234  
Name: Meysam Bijani Zarei  
City of Death: Shahriar  
Province: Tehran  
Date of Death: Unknown  
First Source: X  
Status: Confirmed  

Do this for ALL numbered entries. Do not modify text.


🔹 🔹 Step 4 — Generate Excel datasets

Run the prompt separately for each appendix:

✅ Output:

/data/processed/children.xlsx
/data/processed/adults.xlsx
/data/processed/non_protesting.xlsx


🔹 🔹 Step 5 — Data cleaning (critical)

Normalize:
spacing
line breaks
multi-line entries
Ensure:
1 row = 1 numbered entry
all 7 columns populated

🔹 🔹 Step 6 - Detect duplicate names

Check duplicates in Name column only

Count:
total duplicate rows
distinct duplicated names

⚠️ Important:

Name ≠ unique identifier
Used only for baseline analysis

✅ Output:

/analysis/duplicate_names.xlsx
183 entries found >> which initially means 92 people may be repeated twice

🔹 🔹 Step 7 - in the duplicate names, look into column (City of Death), remove names that are duplicate but are confimred in diffrenet cities.
This results 32 people who are not duplictes, removing tehse from  step 6 results

183-34  = 149 names (all repeated twice) +  one name repated three times) >> 150 duplicand 75 people seem to be duplicated.

✅ ✅ ✅ ✅ ✅ ✅ ✅ ✅
Results
75 duplicates in 4,162 (Adults) and no duplicates in 236 children. Details of 75 Duplicates found are lsited here (open to be corss examined),

The Preliminary Verdict, the 400 to 500 Ms BaBaali claims is far from accurate

The Duplicate list
The first number if HRANA appendix ID of that name

733	Abedin Khazaei	Karaj (Fardis)	Alborz	
4104	Abedin Khazaei	Karaj	Alborz	

1200	Abolfazl Eskandari	Arak	Markazi	
3949	Abolfazl Eskandari	Arak	Markazi	

54	Abolfazl Khaledi	Lordegan	Chaharmahal and Bakhtiari
1757	Abolfazl Khaledi	Unknown

385	  Abolghasem Babaei	Tehran (Vahidiyeh)	Tehran	
1778	Abolghasem Babaei	Unknown

362	  Ahmad Asgari	Karaj	Alborz	January 8, 2026 (1404/10/18)
3956	Ahmad Asgari	Karaj	Alborz	Unknown

963	  Ahmad Ramazanzadeh	Mashhad	Khorasan Razavi	
1804	Ahmad Ramazanzadeh	Unknown	

1861	Akbar Pashapour	Unknown	
3914	Akbar Pashapour	Mohammadshahr	Alborz

227	  Ali Abbasi	Tehran	Tehran	
1364	Ali Abbasi	Mashhad (Toos)	Khorasan Razavi	Unknown

4124	Ali Ataei	Tehran	Tehran	Unknown
2939	Ali Ataei	Unknown	Unknown	Unknown

2953	Ali Karimi	Eshtehard	Alborz	January 8, 2026 (1404/10/18)
2091	Ali Karimi	Falavarjan	Isfahan	January 8, 2026 (1404/10/18)

457	  Ali Moradi	Karaj	Alborz	January 8, 2026 (1404/10/18)
1537	Ali Moradi	Karaj	Alborz	January 9, 2026 (1404/10/19)

2977	Alireza Orooji	Unknown
3009	Alireza Orooji	Unknown

3001	Alireza Seyed Saleh	Unknown	
551	  Alireza Seyed Saleh	Unknown	Isfahan	January 8, 2026 (1404/10/18)

3894	Amirali Molaei	Qeshm	Hormozgan	
2019	Amirali Molaei	Unknown	Unknown

1971	Amirhossein Mirzaei	Gorgan	Golestan	Unknown
1194	Amirhossein Mirzaei	Gorgan	Golestan	January 8, 2026 (1404/10/18)

1127	Arshan Ghasemi	Tehran (Haft Tir Square)	Tehran	January 8, 2026 (1404/10/18)
1520	Arshan Ghasemi	Unknown

3967	Arshia Rashidian	Karaj	Alborz	Unknown
4107	Arshia Rashidian	Karaj	Alborz	

2243	Ataollah Ebrahimpour Ghaziani	Unknown	
2852	Ataollah Ebrahimpour Ghaziani	Tehran (Narmak)	Tehran	

495  	Azizollah Monfared	Neyshabur	Razavi Khorasan	January 8, 2026 (1404/10/18)
2850	Azizollah Monfared	Unknown	

40	Bahram Zahedi	Rasht	Gilan	January 8, 2026 (1404/10/18)
3180	Bahram Zahedi	Rasht	Gilan	January 9, 2026 (1404/10/19)

1728	Behnam Ebrahimian	Karaj (Andisheh Town)	Alborz	January 9, 2026 (1404/10/19)
2139	Behnam Ebrahimian	Unknown	

2143	Behnam Mirzaei	Unknown	
1185	Behnam Mirzaei	Tehran (District 18, Persian Gulf Boulevard)	Tehran	January 8, 2026 (1404/10/18)

2843	Erfan Alizadeh	Unknown	
93	  Erfan Alizadeh	Varamin	Tehran

599	  Farhad Balashzar	Kermanshah	Kermanshah	Unknown
3088	Farhad Balashzar	Unknown	

680	  Hajar Eshaghi	Isfahan	Isfahan	January 9, 2026 (1404/10/19)
3477	Hajar Eshaghi	Unknown	

1286	Hassan Alizadeh	Rasht (Moallem Boulevard, in front of Governorate)	Gilan	January 8, 2026 (1404/10/18)
2281	Hassan Alizadeh	

2324	Hossein Gholami	Unknown	
2325	Hossein Gholami	Unknown

2311	Hossein Soleimani	
2312	Hossein Soleimani

1636	Hossein Tehranchi	Tehran	Tehran	January 8, 2026 (1404/10/18)
1487	Hossein Tehranchi	Tehran (Narmak)	Tehran	January 8, 2026 (1404/10/18)

2335	Hossein Yaghmaei	Unknown	
407	  Hossein Yaghmaei	Khorramabad	Lorestan	Unknown

2230	Javad Ganji	Unknown		
57	  Javad Ganji	Tehran	Tehran	January 9, 2026 (1404/10/19)

43	  Khaled Molaei	Bandar Abbas	Hormozgan	January 8, 2026 (1404/10/18)
2385	Khaled Molaei	Unknown		

2388	Khodadad Sarlak Chivai	Unknown	
4050	Khodadad Sarlak Chivai	Isfahan	Isfahan	Unknown

4161	Mahan Kargar	Isfahan	Isfahan	
3932	Mahan Kargar	Khomeini Shahr	Isfahan	

1446	Majid Asgharnezhad	Amol	Mazandaran	January 9, 2026 (1404/10/19)
4084	Majid Asgharnezhad	Amol	Mazandaran	Unknown

1264	Mansour Shahsavari	Aligudarz (in front of Seminary)	Lorestan	January 8, 2026 (1404/10/18)
2835	Mansour Shahsavari	Aligoudarz	Lorestan	Unknown

******* tripple mention
339	  Masoud Faghihzadeh	Isfahan (Khaghani Area)	Isfahan	Unknown
1219	Masoud Faghihzadeh	Isfahan (Khaghani)	Isfahan	January 8, 2026 (1404/10/18)
2014	Masoud Faghihzadeh	Isfahan	Isfahan	Unknown
******* 

616	  Mehdi Jafari	Unknown		
3870	Mehdi Jafari	Karaj (Mehrshahr)	Alborz	January 9, 2026 (1404/10/19)

115	  Mehdi Lavasani	Tehran	Tehran	Unknown
2633	Mehdi Lavasani	Tehran	Tehran	

1010	Mehdi Mostafaei Pour	Unknown	Unknown	January 8, 2026 (1404/10/18)
3692	Mehdi Mostafaei Pour	Unknown	Unknown	Unknown

3651	Mehdi Sanaei Samani	Unknown	
1207	Mehdi Sanaei Samani	Saman	Chaharmahal and Bakhtiari	January 9, 2026 (1404/10/19)

4072	Mohammad Amin Majidi	Azadshahr	Golestan	January 8, 2026 (1404/10/18)
3349	Mohammad Amin Majidi	Unknown		

3304	Mohammad Golriz	Unknown		
378	  Mohammad Golriz	Tehran (Andarzgoo Boulevard)	Tehran	January 9, 2026 (1404/10/19)

4062	Mohammad Mehdi Jarchi	Karaj	Alborz	January 9, 2026 (1404/10/19)
3471	Mohammad Mehdi Jarchi	Unknown
	
3393	Mohammad Reza Ahmadi			
3394	Mohammad Reza Ahmadi
		
484	  Mohammad Rezaei	Tehran	Tehran	Unknown
3269	Mohammad Rezaei	Unknown	Unknown	January 8, 2026 (1404/10/18)

2714	Mohammad Rezaei Navid	Shahriar	Tehran	January 8, 2026 (1404/10/18)
3271	Mohammad Rezaei Navid	Shahriar (Ferdowsi)	Tehran	

3277	Mohammad Zare	Unknown		
3276	Mohammad Zare	Unknown	January 9, 2026 (1404/10/19)

1199	Mojtaba Hashempour Pashaki	Tehran	Tehran	Unknown
3174	Mojtaba Hashempour Pashaki	Unknown	

3512	Morteza Aghaei	Unknown		January 8, 2026 (1404/10/18)
2008	Morteza Aghaei	Tehran	Tehran	January 7, 2026 (1404/10/17)

3525	Morteza Rahnama Topkanlou	Chenaran	Razavi Khorasan	Unknown
3526	Morteza Rahnama Topkanlou	Unknown		

3593	Mostafa Mirzaei	Unknown	Unknown	January 8, 2026 (1404/10/18)
1130	Mostafa Mirzaei	Tehran (Yaftabad)	Tehran	January 8, 2026 (1404/10/18)

3784	Naser Khoshnoudi Najaf Abadi	Najafabad	Isfahan	Unknown
3783	Naser Khoshnoudi Najaf Abadi	Unknown
	
3801	Navid Mirzaei	Unknown		
604	  Navid Mirzaei	Eslamabad	Kermanshah	

3803	Nima Palizgar	Unknown		January 8, 2026 (1404/10/18)
264	  Nima Palizgar	Fardis	Alborz	January 8, 2026 (1404/10/18)

4041	Omid Abbasi	Tehran	Tehran	Unknown
1704	Omid Abbasi	Fardis	Alborz	January 8, 2026 (1404/10/18)

471	  Parsa Abbaspour	Fardis	Alborz	Unknown
4017	Parsa Abbaspour	Karaj	Alborz	Unknown

2482	Reza Gholipour	Unknown		
2481	Reza Gholipour	Unknown		January 8, 2026 (1404/10/18)

1727	Reza Habibi	Karaj (Andisheh Town)	Alborz	Unknown
728	  Reza Habibi	Shiraz	Fars	January 9, 2026 (1404/10/19)

1305	Reza Kavousi Heydari	Fooladshahr	Isfahan	Unknown
2485	Reza Kavousi Heydari	Unknown		January 9, 2026 (1404/10/19)

581	  Reza Khanzadeh	Esfarayen	North Khorasan	Unknown
2464	Reza Khanzadeh	Unknown

2511	Roya Nouri Ziarani	Unknown	
3923	Roya Nouri Ziarani	Karaj	Alborz	January 9, 2026 (1404/10/19)

1215	Saeed Taghvai	Arak	Markazi	Unknown
2583	Saeed Taghvai	Unknown	

4066	Saman Delaram	Pardis	Tehran	January 9, 2026 (1404/10/19)
1237	Saman Delaram	Pardis	Tehran	

2328	Seyed Abdollah Zamani	
2689	Seyed Abdollah Zamani

4087	Seyed Ahmad Kazemi	Bandar Abbas	Hormozgan	January 9, 2026 (1404/10/19)
492	  Seyed Ahmad Kazemi	Bandar Abbas	Hormozgan	January 8, 2026 (1404/10/18)

515	  Seyed Akbar Hosseini	Tehran	Tehran	Unknown
2651	Seyed Akbar Hosseini	Unknown

4088	Seyed Hamid Salehi	Qarchak	Tehran	Unknown
2674	Seyed Hamid Salehi	Unknown

4093	Seyed Milad Hosseini	Tehran	Tehran	Unknown
2737	Seyed Milad Hosseini	Unknown

2705	Seyed Mohammad Hosseini	Rasht	Gilan	Unknown
2707	Seyed Mohammad Hosseini	Unknown

2710	Seyed Mohammad Mousavi	
2709	Seyed Mohammad Mousavi	

2718	Seyed Mohammadreza Mousavi	Unknown
500	  Seyed Mohammadreza Mousavi	Tehran	

2727	Seyed Moslem Fatemi	Unknown
1599	Seyed Moslem Fatemi	Rasht	Gilan	

2681	Seyed Saeed Parvar	Unknown
1531	Seyed Saeed Parvar	Tehran	Tehran	

290	  Shahin Azar Atash	Unknown	Gilan	
4095	Shahin Azar Atash	Astaneh Ashrafiyeh	Gilan	

2763	Shirzad Balaei	Unknown
252	  Shirzad Balaei	Islamabad-e Gharb	Kermanshah	January 8, 2026 (1404/10/18)

913	  Yadollah Eskandari	Arsanjan	Fars	Unknown
3849	Yadollah Eskandari	Unknown		
