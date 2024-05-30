*{{date:Do MMM YYYY}}*
# Standup
### Today
- [ ] 
### Blockers
- 
# Tasks
#### Done day before:
```tasks
filter by function task.done.moment?.isSame(moment("{{date:YYYY-MM-DD}}").subtract(1, 'days'), 'day') || false
filter by function task.status.symbol === 'x'
```
## In progress
```tasks
path includes {{query.file.folder}}
filter by function task.status.symbol === '/'
```
## By due date
```tasks
path includes {{query.file.folder}}
sort by priority
sort by due
not done
hide start date
hide urgency
filter by function task.status.symbol !== '/'
limit 100
group by function \
	const date = task.due.moment; \
	return \
	(!date) ? '%%4%% No due date' : \
	!date.isValid() ? '%%0%% Invalid date' : \
	date.isBefore(moment(), 'day') ? '%%1%% Overdue!' : \
	date.isSame(moment(), 'day') ? '%%2%% Today' : \
	'%%3%% Future';
```
