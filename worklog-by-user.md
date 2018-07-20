# Worklog by a user on date
This jql is for listing the issues having a USER added worklogs on DATE

```sql
worklogDate=DATE AND worklogAuthor=USER
```
This is very useful for implementing the integration between company's billing system and JIRA.

## Example
This is the pseudo codes, not properly tested.

```perl
package modules::JIRA;
use LWP::UserAgent;
use JSON;

sub getUserWorklog {

    my $self = shift;
    my $args = shift || {};
    my $params = {
        jql    => "worklogDate=$args->{date} AND worklogAuthor=$args->{userName}",
        fields => ['summary', 'assignee', 'reporter', 'duedate', 'worklog', 'created']
    };
    
    # Assume that the authentication is already working.
    my $ua = LWP::UserAgent->new();  
    my $res = $ua->post(
        'JIRA_BASE_URL/rest/api/2/search',
        'Content-Type' => 'application/json',
        'Content' => to_json($params)
    );
    
    my $data = $res->content(); # This will list all the issues matched with the jql
    my @output;
    
    foreach my $issue ( @{$data} ){    
        #Only get the user's worklog of the $issue
        foreach my $worklog @{ $issue->{fields}{worklogs} ) {
            if( $worklog->{author}{key} eq $args->{userName} && $worklog->{started} eq $args->{date} ) {
                push @output, $worklog;
            }
        }
    }

    return to_json( \@output);

}

```
Call a function
```
my $jiea = new modules::JIRA;
my $worklogs = $jira-getWorklog({ user=> "yoda", date=> "2018-07-20" });
```
