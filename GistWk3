//1. Create a Trigger that processes after insert and after update on Lead
//LeadTrigger
trigger LeadTrigger on Lead (after insert, after update) {
    if (trigger.isInsert) {
        if (trigger.isAfter) {
            LeadTriggerHandler.handleAfterInsert(trigger.new);
        }
    } else if (trigger.isUpdate) {
        if (trigger.isAfter) {
            LeadTriggerHandler.handleAfterUpdate(trigger.new, trigger.oldMap, Trigger.newMap);
        }
    }
}

//2.Create a Handler class for your trigger that contains all the trigger logic
//After Insert & After Update Handling
//Based on a Lead’s Product Interest, create a task to follow up with the lead.
//However, If the trigger is firing on after update, we only want to create a task if the product interest has changed.  Otherwise we’ll get a new task every time the lead is edited in any way!
 public with sharing class LeadTriggerHandler {
    public static void handleAfterInsert(List<Lead> newLeads) {
        List <Task> TasksToInsert = New list<Task>();
         // Methods for LeadTrigger handler logic
     //List<Lead> NewListLead = newLeads;
        for(Lead ld : newLeads) {
           Task TT =New Task();
            TT.whoId=ld.Id;
            TT.subject = ld.Company;
            TT.Priority = 'High';
            TasksToInsert.add(TT);  
        }
        system.Debug(TasksToInsert);
         Insert TasksToInsert;
    }

    public static void handleAfterUpdate(List<Lead> newLeads, Map<ID, Lead> oldLeadMap,Map<ID, Lead> NewLeadMap ) {
         List <Task> TasksToInsert = New list<Task>();
             // Methods for LeadTrigger handler logic
         //List<Lead> NewListLead = newLeads;
            for(Lead ld : newLeads) {
               Lead OldLead =  oldLeadMap.get(ld.id);
                if (ld.ProductInterest__c == oldlead.ProductInterest__c) {
                    continue;
                }
               Task TT =New Task();
                TT.whoId=ld.Id;
                TT.subject = ld.Company;
                TT.Priority = 'High';
                TasksToInsert.add(TT);  
            }
            system.Debug(TasksToInsert);
             Insert TasksToInsert;
             
    }
}
