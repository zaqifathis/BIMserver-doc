#summary How to write Service plugins

= Introduction =

Service plugins can extend the functionality of a BIMserver by listening to notifications and acting upon them. For example a ClashDetection Service plugin could create a ClashDetection report as [ExtendedData] when a user checks in a new revision.

= Details =

For this plugin you do not need implement any specific methods as long as you subclass [ServicePlugin]. You can register your services by calling the [register] method:

{{{
public void register(ServerDescriptor serverDescriptor, ServiceDescriptor serviceDescriptor, NotificationInterface notificationInterface) {
}
}}}

It's best to register your services in the init method. You have to provide a [ServerDescriptor] and [ServiceDescriptor], here are examples for those:

{{{
ServerDescriptor serverDescriptor = StoreFactory.eINSTANCE.createServerDescriptor();
serverDescriptor.setTitle("Clashdetection");
		
ServiceDescriptor clashDetection = StoreFactory.eINSTANCE.createServiceDescriptor();
clashDetection.setName("Clashdetection");
clashDetection.setDescription("Clashdetection");
		clashDetection.setNotificationProtocol(AccessMethod.INTERNAL);
clashDetection.setReadRevision(true);
clashDetection.setWriteExtendedData(true);
clashDetection.setTrigger(Trigger.NEW_REVISION);
}}}

Example implementation code:

{{{
register(serverDescriptor, clashDetection, new NotificationInterfaceAdapter(){
	@Override
	public void newLogAction(SLogAction newRevisionNotification, SToken token, String apiUrl) throws UserException, ServerException {
		ServiceInterface serviceInterface = getServiceInterface(token);
		// Here goes your code
	}
}
}}}