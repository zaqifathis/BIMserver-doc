Since version 1.5.88 any BIMserver instance is capable of running services on models that are not necessarily stored on that specific instance. This is utilizing the BimBot interface which is a lot leaner than the previous protocol for inter-BIMserver communication.

The previous protocol basically only support sending/receiving notifications which contained the proper credentials to subsequently use the BIMserver API to query the model. Services could optionally attach extended data to a revision, but were not required to do so.

The BimBots interface is a little more strict in the sense that it has a pre-defined input _and_ output. For this reason, writing services in BIMserver that can be run as a BimBit is slightly different, but existing services can be easily retrofitted and that's what's described on this page.

