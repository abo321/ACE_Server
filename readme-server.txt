1. server1
    MyTask, Handler
    exit when timeout, by calling ACE_Reactor::notify, user-defined notify, or wakeup_all_threads to exit
    provide menu for user
	
    ��ʱ������ACE_Reactor::notify()�����Զ����notify������wakeup_all_threads�˳�

2. server2
    MyTask, MyTask2, Handler
    MyTask timeout, then spawn MyTask2
    MyTask2 register/remove ACE_STDIN handler 2 times
    exit according to the number of timeout (2 times)
    provide menu for user
	
    ��ʱʱע��/ɾ��ACE_STDIN��handler��2�Σ���2�γ�ʱʱ�˳�������2�γ�ʱʱע��/ɾ��ACE_STDIN��handler��Ȼ���У�ֻ����MyTask�˳����ٴ���ע��/ɾ�����¼��ˣ�

3. server21
    MyTask, MyTask2, Handler
    MyTask timeout, then spawn MyTask2
    MyTask2 register ACE_STDIN handler 3 times
    exit according to the number of timeout (2 times)
    provide menu for user

    ��ʱʱע��ACE_STDIN��handler 2�Σ���2�γ�ʱʱ�˳�������2�γ�ʱʱע��ACE_STDIN��handler��Ȼ���У�ֻ����MyTask�˳����ٴ���ע����¼��ˣ�

4. server22
    MyTask, MyTask2, Handler
    MyTask timeout, set the exit flag, then spawn MyTask2
    MyTask2 register ACE_STDIN handler 1 times, then the registeration will wakeup the wait-state thread
    then MyTask exit according to the eixt flag
    provide menu for user

    ��ʱʱ�����˳���־����ע��ACE_STDIN��handler����ע�ᶯ������handle_events�����ݱ�־�˳�
 
5. server3
    MyTask, Handler, timeout, wakeup_all_threads to exit
	
    ��ʱʱ�����˳���־����ֱ�ӵ���wakeup_all_threads����handle_events�����ݱ�־�˳�

6. server4
    MyTask, Handler, timeout, wakeup_all_threads to exit
    provide menu for user
	
    ��ʱʱ�����˳���־����ֱ�ӵ���wakeup_all_threads����handle_events�����ݱ�־�˳�

7. server5
    MyTask, no Handler, in svc, receive data directly by ACE_SOCK_Dgram, timeout to exit
    provide menu for user

    û��Handler����ʹ��ACE_Reactor��handle_events��ֱ��ʹ��ACE_SOCK_Dgram����/�������ݣ��ҳ�ʱʱֱ��break�˳�

8. server6
    MyTask, no Handler, in svc, use select (Linux system call) to wait event, receive data directly by ACE_SOCK_Dgram, timeout to exit
    provide menu for user

    û��Handler����ʹ��ACE_Reactor��handle_events��ֱ�ӵ���Linuxϵͳ����select���˿�״̬���������ݵ�������ʹ��ACE_SOCK_Dgram�������ݣ��ҳ�ʱʱ�����˳���־�����ݱ�־�˳�

9. server7
    implement ACE_Reactor with ACE_Select_Reactor_T
    MyTask, Handler, timeout, wakeup_all_threads to exit
    provide menu for user

    ֱ��ʹ��ACE_Select_Reactor����ʱʱ�����˳���־����ֱ�ӵ���wakeup_all_threads����handle_events�����ݱ�־�˳�

10. server8
    implement ACE_Reactor with ACE_Select_Reactor_T
    MyTask, MyTask2, Handler
    MyTask has no timeout
    MyTask spawn MyTask2 before the forever-loop handle_events
    MyTask2 register/remove user-defined handler 2 times
    exit according to the number of receive data package
    provide menu for user

    ��ʾʹ��ACE_Select_Reactorʵ��ACE_Reactor����MyTask��svc�����е�����ѭ��ǰ����MyTask2����MyTask�е�handle_eventsû�г�ʱ��MyTask2ע��/ɾ���Զ����handler 2�Ρ�MyTask�յ�client��2�����ݰ��˳���

11. server81
    implement ACE_Reactor with ACE_Select_Reactor_T
    MyTask, MyTask2, Handler
    MyTask has no timeout
    MyTask spawn MyTask2 before the forever-loop handle_events
    MyTask2 register/remove ACE_STDIN handler 2 times
    exit according to the number of receive data package
    provide menu for user

    ��ʾʹ��ACE_Select_Reactorʵ��ACE_Reactor����MyTask��svc�����е�����ѭ��ǰ����MyTask2����MyTask�е�handle_eventsû�г�ʱ��MyTask2ע��/ɾ��ACE_STDIN��handler 2�Ρ�MyTask�յ�client��2�����ݰ��˳���

12. server82
    implement ACE_Reactor with ACE_Select_Reactor_T
    MyTask, MyTask2, Handler
    MyTask has no timeout
    MyTask spawn MyTask2 before the forever-loop handle_events
    MyTask2 register/remove signal handler 2 times
    exit according to the number of receive data package
    provide menu for user

    ��ʾʹ��ACE_Select_Reactorʵ��ACE_Reactor����MyTask��svc�����е�����ѭ��ǰ����MyTask2����MyTask�е�handle_eventsû�г�ʱ��MyTask2ע��/ɾ��signal��handler 2�Ρ�MyTask�յ�client��2�����ݰ��˳���

13. server99
    implement ACE_Reactor with ACE_Select_Reactor_T
    MyTask, MyTask2, Handler
    MyTask has no timeout
    MyTask spawn MyTask2 before the forever-loop handle_events
    MyTask2 register/remove given ACE_HANDLE value handler such as 1023 2 times
    using notify the given ACE_HANDLE value handler to exit according to the number of receive data package
    provide menu for user

    ��ʾʹ��ACE_Select_Reactorʵ��ACE_Reactor����MyTask��svc�����е�����ѭ��ǰ����MyTask2����MyTask::svc�е�handle_eventsû�г�ʱ��
    MyTask2ע��/ɾ������ֵ��handler������1023��2�Ρ�MyTask�յ�client��2�����ݰ�ʱ����ACE_Reactor::notify��������ʹ��ACE_Event_Handler::EXCEPT_MASK���������ڸ�mask��Ӧ�Ĵ�����handle_exception�������˳���־�������ݸñ�־�˳�MyTask��
    MyTask::svc�е�ACE_Reactor��Handler�����Ǿֲ�����selector��MyTask�������
    MyTask��MyTask2����ACE_Singleton����

14. server98

    implement ACE_Reactor with ACE_Select_Reactor_T
    MyTask, MyTask2, Handler
    MyTask has no timeout
    MyTask spawn MyTask2 before the forever-loop handle_events
    MyTask2 register/remove given ACE_HANDLE value handler such as 1023 2 times
    using notify the given ACE_HANDLE value handler to exit according to the number of receive data package
    ACE_singleton task is not used, Reactor, Selector is data member of MyTask
    mytask is a local object, the destruction of Reactor, Selector is done in ~MyTask
    provide menu for user

    ��ʾʹ��ACE_Select_Reactorʵ��ACE_Reactor����MyTask��svc�����е�����ѭ��ǰ����MyTask2����MyTask::svc�е�handle_eventsû�г�ʱ��
    MyTask2ע��/ɾ������ֵ��handler������1023��2�Ρ�MyTask�յ�client��2�����ݰ�ʱ����ACE_Reactor::notify��������ʹ��ACE_Event_Handler::EXCEPT_MASK���������ڸ�mask��Ӧ�Ĵ�����handle_exception�������˳���־�������ݸñ�־�˳�MyTask��
    MyTask::svc�е�Handler�����Ǿֲ�����reactor��selector��MyTask���������~MyTask���ͷ������������
    MyTask2������MyTask::svc�����еľֲ�����ÿ��MyTask������������������������MyTask����

15. server97

    implement ACE_Reactor with ACE_Select_Reactor_T
    MyTask, MyTask2, Handler
    MyTask has no timeout
    MyTask spawn MyTask2 before the forever-loop handle_events
    MyTask2 register/remove given ACE_HANDLE value handler such as 1023 2 times
    using notify the given ACE_HANDLE value handler to exit according to the number of receive data package
    ACE_singleton task is not used, Reactor, Selector, Hanlder is data member of MyTask
    mytask corresponds to a global object, the destruction of Reactor, Selector is done in MyTask::close
    provide menu for user

    ��ʾʹ��ACE_Select_Reactorʵ��ACE_Reactor����MyTask��svc�����е�����ѭ��ǰ����MyTask2����MyTask::svc�е�handle_eventsû�г�ʱ��
    MyTask2ע��/ɾ������ֵ��handler������1023��2�Ρ�MyTask�յ�client��2�����ݰ�ʱ����ACE_Reactor::notify��������ʹ��ACE_Event_Handler::EXCEPT_MASK���������ڸ�mask��Ӧ�Ĵ�����handle_exception�������˳���־�������ݸñ�־�˳�MyTask��
    reactor, selector��handler����MyTask���������MyTask::close���ͷ������������MyTask2������MyTask::svc�����еľֲ�����
    �ڳ���ʼʱ������MyTask�����Ժ�ÿ������������������ʹ����һ��MyTask����