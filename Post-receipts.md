

export const unpostedReceiptsModule = '/unposted-receipts';

export const unpostedReceipts = `/receiving/unposted-receipts`;

if url match with above two, do post receipts action
props.actions.postUnpostedReceipts--->postReceipts in reducers/receiving/unpostedReceipts/actions--->
service.postReceipts

if url not match with above two, do post receipt
props.actions.postReceipt() ----> postReceipt in reducers/receiving/receipt/actions 








2
I need to create Map<String, String> from List<Person> using Stream API.

persons.stream()
       .collect(Collectors.toMap(Person::getNationality, Person::getName, (name1, name2) -> name1)
But in the above case, I want to resolve conflict in name attribute by using Person's age. is there any way to pass merge function something around the lines (age1, age2) -> // if age1  is greater than age2 return name1, else return name2 ?

8

To select a person based on its age, you need the Person instance to query the age. You cannot reconstitute the information after you mapped the Person to a plain name String.

So you have to collect the persons first, to be able to select the oldest, followed by mapping them to their names:

persons.stream()
    .collect(Collectors.groupingBy(Person::getNationality, Collectors.collectingAndThen(
        Collectors.maxBy(Comparator.comparingInt(Person::getAge)),
        o -> o.get().getName())));



