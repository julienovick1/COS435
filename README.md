# COS 435 Final Project: An Analysis of TEDTalks and Their Accuracy on Ratings

## About
- Our Project: Parse through TEDTalks to find the frequency of our chosen query terms and make conclusions about the talk's popularity, importance of information, etc.

[Project Report](https://docs.google.com/a/princeton.edu/document/d/1SSCkPTsWcfJLbCXR1BfvUc-UPiSH6GS6dpEigx0i74c/edit?usp=sharing)

## The Team
- Professor: Andrea LaPaugh 

- Julie Novick-Lederer (julieen)
- Emily Speyer (espeyer)
- Nicole Marvin (nmarvin)

## Deadlines
- 3/13 Project proposal 
- 4/17 Progress report 
- 5/16 Code and writeup due 
- 5/17-5/19 Demo day 

## Working Code

### parse.py
```markdown

#!/usr/bin/env python
import sys
import os

def main():

	# correct number of arguments
	if len(sys.argv) < 2:
		print "error"
		return

	# command line arguments
	query = sys.argv[1]

	# initialize output
	output = ""

	# open query
	with open(query) as input_file:
		for line in input_file:
			query_term = line.rstrip('\n')

			# iterate through documents
			for document in os.listdir("/Users/Julie/cos435/talks"):
				filename = "/Users/Julie/cos435/talks/" + document
				open_doc = open(filename, 'r')
				doc = open_doc.read()
				word_list = doc.split()

				# initilize variables
				count = 0
				all_data = []

				# count appearance of query term
				freq = doc.count(query_term)

				# total word count
				for w in word_list:
					count += 1

				# percentage of technical words
				percent_tech_words = (float(freq)/float(count)) * 100

				# populate all_data with doc, query_term, freq, count
				all_data.append(str(document))
				all_data.append(str(query_term))
				all_data.append(str(freq))
				all_data.append(str(count))
				all_data.append(str(percent_tech_words))

				# info we want in our output
				output += "\t".join(all_data) + "\n"
	
	# write output to stdout
	sys.stdout.write(output)

main()

```

### parse2.py

```markdown

#!/usr/bin/env python
import sys
import os

def main():

	# correct number of arguments
	if len(sys.argv) < 2:
		print "error"
		return

	# command line arguments
	query = sys.argv[1]

	# initialize output
	output = ""

	# iterate through documents
	for document in os.listdir("/Users/Julie/cos435/talks"):
		filename = "/Users/Julie/cos435/talks/" + document
		open_doc = open(filename, 'r')
		doc = open_doc.read()
		word_list = doc.split()

		# initialize total query count
		query_count = 0
		# initialize word count
		word_count = 0

		# open query
		with open(query) as input_file:
			for line in input_file:
				query_term = line.rstrip('\n')

				# initialize empty array for all data
				all_data = []

				# count appearance of query term
				query_count += doc.count(query_term)

				# total word count
				for w in word_list:
					word_count += 1

				# percentage of query words out of total word count
				percent_query_words = (float(query_count)/float(word_count)) * 100

				# compare values better
				compare_values = percent_query_words * 100

			# populate all_data with document, query_cpimt, percent_query_words
			all_data.append(str(document))
			all_data.append(str(query_count))
			all_data.append(str(percent_query_words))
			all_data.append(str(compare_values))

			# info we want in our output
			output += "\t".join(all_data) + "\n"
	
	# write output to stdout
	sys.stdout.write(output)

main()

```
