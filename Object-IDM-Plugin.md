#summary How to write ObjectIDM plugins

An ObjectIDM helps other code to decide whether to follow a relation/reference or not. This can be used to define subsets of models, based on a given starting point.

{{{
public interface ObjectIDMPlugin extends Plugin {
	ObjectIDM getObjectIDM();
}
}}}

{{{
public interface ObjectIDM {
	boolean shouldFollowReference(EClass originalClass, EClass eClass, EStructuralFeature eStructuralFeature);
	boolean shouldIncludeClass(EClass originalClass, EClass eClass);
}
}}}