---
title: UfiSpace FHG M-plane test

---

# Ufispace FHG mplane

<aside>
Goal: Use Netconf to control the ufispace.


## Access method
:::success
ufispace :   
- IP : 192.168.8.25
- user name : ocnos
- Ocnos Password : ocnos
    
SMO L release :   
- Host zhongkui
-   Hostname 192.168.8.69
-   User ubuntu
:::
    
## Reference:
:::info
1. https://docs.ipinfusion.com/service-provider-6.6/index.html#page/OcNOS_SP/NetConf_Cmds.html
2. https://hackmd.io/@Summer063/ryDBN4Qpn/https%3A%2F%2Fhackmd.io%2F%40q-eiMFW8TLa2Pa3QKECMzw%2FryzwIx5jR#UFISpace
:::

</aside>

---

## M-plane checklist


| Function                             | Description                                | Status  |
| -------------------------------- | --------------------------------------- | ------------- |
| Tools to control ufispace through M-plane | Use NETCONF tools to manage device configs | ✅netopeer2 <br>✅ncclient |
| Get config                       | Retrieve current switch configuration      | ✅ done |
| Shutdown port            | Administratively shut down the port   | ✅ done |
| Enable / Disable port                    | Toggle port state between enable/disable        | ✅ done |
| Setting bridge-group             | Bind port to a specific bridge-group       | ✅ done |
| Setting switch mode trunk        | Configure port mode as trunk               | ✅ done |
| Add VLAN                         | Add VLANs to the trunk or access port      | ✅ done |
| Setting mtu                      | Configure maximum transmission unit size   | ✅ done |



## 1. Get config

### 1.1 Method 1: Use ncclient to control the M-plane

- Create a new file
    
    ```bash
    vim getNetconf.py
    ```
    
    ```python
    from ncclient import manager
    smo = manager.connect(host='192.168.8.25', port="830", timeout=5,
                          username="ocnos", password="ocnos", hostkey_verify=False)
    result = smo.get_config(source="running")
    print(result)
    ```
    
- Run the python file
    
    ```bash
    python3 getNetconf.py > FHG.xml
    ```
    
:::spoiler FHG.xml
```bash
<?xml version="1.0" encoding="UTF-8"?>
<rpc-reply xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0"
  message-id="urn:uuid:71263ba2-ff20-402b-8ab3-c7cfeb98517a"
  last-modified="2025-08-13T08:27:31Z"
  xmlns="urn:ietf:params:xml:ns:netconf:base:1.0">
  <data><netconf-server xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-management-server">
  <vrfs>
    <vrf>
      <vrf-name>default</vrf-name>
      <config>
        <vrf-name>default</vrf-name>
      </config>
      <netconf-ssh-config>
        <config>
          <feature-netconf-ssh>false</feature-netconf-ssh>
        </config>
      </netconf-ssh-config>
      <netconf-tls-config>
        <config>
          <feature-netconf-tls>false</feature-netconf-tls>
        </config>
      </netconf-tls-config>
    </vrf>
    <vrf>
      <vrf-name>management</vrf-name>
      <config>
        <vrf-name>management</vrf-name>
      </config>
      <netconf-ssh-config>
        <config>
          <feature-netconf-ssh>true</feature-netconf-ssh>
        </config>
      </netconf-ssh-config>
      <netconf-tls-config>
        <config>
          <feature-netconf-tls>true</feature-netconf-tls>
        </config>
      </netconf-tls-config>
    </vrf>
  </vrfs>
</netconf-server>
<network-instances xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-network-instance">
  <network-instance>
    <instance-name>default</instance-name>
    <instance-type>vrf</instance-type>
    <config>
      <instance-name>default</instance-name>
      <instance-type>vrf</instance-type>
    </config>
    <vrf xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-vrf">
      <config>
        <vrf-name>default</vrf-name>
      </config>
    </vrf>
  </network-instance>
  <network-instance>
    <instance-name>management</instance-name>
    <instance-type>vrf</instance-type>
    <config>
      <instance-name>management</instance-name>
      <instance-type>vrf</instance-type>
    </config>
    <vrf xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-vrf">
      <config>
        <vrf-name>management</vrf-name>
      </config>
    </vrf>
  </network-instance>
  <network-instance>
    <instance-name>1</instance-name>
    <instance-type>l2ni</instance-type>
    <config>
      <instance-name>1</instance-name>
      <instance-type>l2ni</instance-type>
    </config>
    <bridge xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-bridge">
      <config>
        <protocol>mstp</protocol>
      </config>
      <bridge-ports>
        <interface>
          <name>ge0</name>
          <config>
            <name>ge0</name>
          </config>
        </interface>
        <interface>
          <name>ge2</name>
          <config>
            <name>ge2</name>
          </config>
        </interface>
        <interface>
          <name>xe10</name>
          <config>
            <name>xe10</name>
          </config>
        </interface>
        <interface>
          <name>xe11</name>
          <config>
            <name>xe11</name>
          </config>
        </interface>
        <interface>
          <name>xe12</name>
          <config>
            <name>xe12</name>
          </config>
        </interface>
        <interface>
          <name>xe13</name>
          <config>
            <name>xe13</name>
          </config>
        </interface>
        <interface>
          <name>xe14</name>
          <config>
            <name>xe14</name>
          </config>
        </interface>
        <interface>
          <name>xe15</name>
          <config>
            <name>xe15</name>
          </config>
        </interface>
        <interface>
          <name>xe16</name>
          <config>
            <name>xe16</name>
          </config>
        </interface>
        <interface>
          <name>xe17</name>
          <config>
            <name>xe17</name>
          </config>
        </interface>
        <interface>
          <name>xe18</name>
          <config>
            <name>xe18</name>
          </config>
        </interface>
        <interface>
          <name>xe19</name>
          <config>
            <name>xe19</name>
          </config>
        </interface>
        <interface>
          <name>xe6</name>
          <config>
            <name>xe6</name>
          </config>
        </interface>
        <interface>
          <name>xe7</name>
          <config>
            <name>xe7</name>
          </config>
        </interface>
        <interface>
          <name>xe8</name>
          <config>
            <name>xe8</name>
          </config>
        </interface>
        <interface>
          <name>xe9</name>
          <config>
            <name>xe9</name>
          </config>
        </interface>
      </bridge-ports>
      <vlans xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-vlan">
        <vlan>
          <vlan-id>2</vlan-id>
          <config>
            <vlan-id>2</vlan-id>
          </config>
          <customer-vlan>
            <config>
              <type>customer</type>
              <state>enable</state>
            </config>
          </customer-vlan>
        </vlan>
        <vlan>
          <vlan-id>3</vlan-id>
          <config>
            <vlan-id>3</vlan-id>
          </config>
          <customer-vlan>
            <config>
              <type>customer</type>
              <state>enable</state>
            </config>
          </customer-vlan>
        </vlan>
        <vlan>
          <vlan-id>4</vlan-id>
          <config>
            <vlan-id>4</vlan-id>
          </config>
          <customer-vlan>
            <config>
              <type>customer</type>
              <state>enable</state>
            </config>
          </customer-vlan>
        </vlan>
        <vlan>
          <vlan-id>5</vlan-id>
          <config>
            <vlan-id>5</vlan-id>
          </config>
          <customer-vlan>
            <config>
              <type>customer</type>
              <state>enable</state>
            </config>
          </customer-vlan>
        </vlan>
        <vlan>
          <vlan-id>6</vlan-id>
          <config>
            <vlan-id>6</vlan-id>
          </config>
          <customer-vlan>
            <config>
              <type>customer</type>
              <state>enable</state>
            </config>
          </customer-vlan>
        </vlan>
        <vlan>
          <vlan-id>7</vlan-id>
          <config>
            <vlan-id>7</vlan-id>
          </config>
          <customer-vlan>
            <config>
              <type>customer</type>
              <state>enable</state>
            </config>
          </customer-vlan>
        </vlan>
      </vlans>
    </bridge>
  </network-instance>
</network-instances>
<interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface">
  <interface>
    <name>ce20</name>
    <config>
      <name>ce20</name>
    </config>
  </interface>
  <interface>
    <name>ce21</name>
    <config>
      <name>ce21</name>
    </config>
  </interface>
  <interface>
    <name>eth0</name>
    <config>
      <name>eth0</name>
      <vrf-name>management</vrf-name>
    </config>
    <ipv4 xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-ip">
      <config>
        <enable-dhcp-ip-address></enable-dhcp-ip-address>
      </config>
    </ipv4>
  </interface>
  <interface>
    <name>ge0</name>
    <config>
      <name>ge0</name>
      <enable-switchport></enable-switchport>
    </config>
  </interface>
  <interface>
    <name>ge1</name>
    <config>
      <name>ge1</name>
      <enable-switchport></enable-switchport>
    </config>
  </interface>
  <interface>
    <name>ge2</name>
    <config>
      <name>ge2</name>
      <enable-switchport></enable-switchport>
    </config>
  </interface>
  <interface>
    <name>ge3</name>
    <config>
      <name>ge3</name>
    </config>
  </interface>
  <interface>
    <name>lo</name>
    <config>
      <name>lo</name>
    </config>
    <ipv4 xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-ip">
      <config>
        <primary-ip-addr>127.0.0.1/8</primary-ip-addr>
      </config>
    </ipv4>
    <ipv6 xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-ip">
      <addresses>
        <ipv6-address>::1/128</ipv6-address>
        <config>
          <ipv6-address>::1/128</ipv6-address>
        </config>
      </addresses>
    </ipv6>
  </interface>
  <interface>
    <name>lo.management</name>
    <config>
      <name>lo.management</name>
      <vrf-name>management</vrf-name>
    </config>
    <ipv4 xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-ip">
      <config>
        <primary-ip-addr>127.0.0.1/8</primary-ip-addr>
      </config>
    </ipv4>
    <ipv6 xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-ip">
      <addresses>
        <ipv6-address>::1/128</ipv6-address>
        <config>
          <ipv6-address>::1/128</ipv6-address>
        </config>
      </addresses>
    </ipv6>
  </interface>
  <interface>
    <name>xe10</name>
    <config>
      <name>xe10</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2,4-7</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe11</name>
    <config>
      <name>xe11</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>3</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe12</name>
    <config>
      <name>xe12</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2,4-7</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe13</name>
    <config>
      <name>xe13</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>4</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe14</name>
    <config>
      <name>xe14</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>3</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe15</name>
    <config>
      <name>xe15</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>5</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe16</name>
    <config>
      <name>xe16</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2,4-7</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe17</name>
    <config>
      <name>xe17</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>6</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe18</name>
    <config>
      <name>xe18</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2,4-7</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe19</name>
    <config>
      <name>xe19</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>7</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe4</name>
    <config>
      <name>xe4</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
  </interface>
  <interface>
    <name>xe5</name>
    <config>
      <name>xe5</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
  </interface>
  <interface>
    <name>xe6</name>
    <config>
      <name>xe6</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe7</name>
    <config>
      <name>xe7</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe8</name>
    <config>
      <name>xe8</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2,4-7</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <interface>
    <name>xe9</name>
    <config>
      <name>xe9</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2-4</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
  <port-group-speed-map xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-extended">
    <group-index>1</group-index>
    <config>
      <group-index>1</group-index>
      <group-speed>10g</group-speed>
    </config>
  </port-group-speed-map>
  <port-group-speed-map xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-extended">
    <group-index>2</group-index>
    <config>
      <group-index>2</group-index>
      <group-speed>10g</group-speed>
    </config>
  </port-group-speed-map>
  <global xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-if-extended">
    <error-disable>
      <config>
        <error-disable-stp-bpdu-guard>true</error-disable-stp-bpdu-guard>
      </config>
    </error-disable>
  </global>
</interfaces>
<synce xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-synce">
  <globals>
    <config>
      <enable></enable>
      <network-option>1</network-option>
    </config>
  </globals>
  <interfaces>
    <interface>
      <name>ge0</name>
      <config>
        <name>ge0</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>ge2</name>
      <config>
        <name>ge2</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe10</name>
      <config>
        <name>xe10</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe11</name>
      <config>
        <name>xe11</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe12</name>
      <config>
        <name>xe12</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe13</name>
      <config>
        <name>xe13</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe14</name>
      <config>
        <name>xe14</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe15</name>
      <config>
        <name>xe15</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe16</name>
      <config>
        <name>xe16</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe17</name>
      <config>
        <name>xe17</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe18</name>
      <config>
        <name>xe18</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe19</name>
      <config>
        <name>xe19</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe6</name>
      <config>
        <name>xe6</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe7</name>
      <config>
        <name>xe7</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe8</name>
      <config>
        <name>xe8</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
    <interface>
      <name>xe9</name>
      <config>
        <name>xe9</name>
        <enable></enable>
        <synchronous-mode>synchronous</synchronous-mode>
        <is-output-source>true</is-output-source>
      </config>
    </interface>
  </interfaces>
  <external-interfaces>
    <external-interface>
      <external-synce-interface>gps</external-synce-interface>
      <config>
        <external-synce-interface>gps</external-synce-interface>
        <synchronous-mode>synchronous</synchronous-mode>
        <input-source-priority>1</input-source-priority>
        <wait-to-restore-timer>1</wait-to-restore-timer>
        <quality-level>QL_PRC</quality-level>
      </config>
    </external-interface>
  </external-interfaces>
</synce>
<trigger-failover xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-tfo">
  <config>
    <admin-status>disable</admin-status>
  </config>
</trigger-failover>
<logging xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-logging">
  <remote-logging>
    <config>
      <enable-rsyslog></enable-rsyslog>
    </config>
  </remote-logging>
</logging>
<ssh-server xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-ssh">
  <vrfs>
    <vrf>
      <vrf-name>default</vrf-name>
      <config>
        <vrf-name>default</vrf-name>
        <enable>false</enable>
      </config>
    </vrf>
    <vrf>
      <vrf-name>management</vrf-name>
      <config>
        <vrf-name>management</vrf-name>
        <enable>true</enable>
      </config>
    </vrf>
  </vrfs>
</ssh-server>
<telnet-server xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-telnet">
  <vrfs>
    <vrf>
      <vrf-name>default</vrf-name>
      <config>
        <vrf-name>default</vrf-name>
        <enable>false</enable>
      </config>
    </vrf>
    <vrf>
      <vrf-name>management</vrf-name>
      <config>
        <vrf-name>management</vrf-name>
        <enable>true</enable>
      </config>
    </vrf>
  </vrfs>
</telnet-server>
<ntp xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-ntp">
  <vrfs>
    <vrf>
      <vrf-name>management</vrf-name>
      <config>
        <vrf-name>management</vrf-name>
        <feature-enable>true</feature-enable>
        <enable-ntp>true</enable-ntp>
      </config>
    </vrf>
  </vrfs>
</ntp>
<dns-relay xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-dns-relay">
  <config>
    <enable-dns-feature>true</enable-dns-feature>
    <enable-dnsv4-relay>true</enable-dnsv4-relay>
    <enable-dnsv6-relay>true</enable-dnsv6-relay>
  </config>
</dns-relay>
<dns xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-dns-client">
  <vrfs>
    <vrf>
      <vrf-name>management</vrf-name>
      <config>
        <vrf-name>management</vrf-name>
        <lookup-enabled></lookup-enabled>
      </config>
    </vrf>
  </vrfs>
</dns>
<snmp xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-snmp">
  <server-traps>
    <config>
      <enable-link-down-trap>true</enable-link-down-trap>
      <enable-link-up-trap>true</enable-link-up-trap>
    </config>
  </server-traps>
  <servers xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-snmp-server">
    <server>
      <vrf-name>management</vrf-name>
      <config>
        <vrf-name>management</vrf-name>
        <enabled></enabled>
      </config>
      <snmp-views xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-snmp-server-extended">
        <snmp-view>
          <view-name>all</view-name>
          <config>
            <view-name>all</view-name>
          </config>
          <oid-trees>
            <oid-tree>
              <oid>.1</oid>
              <config>
                <oid>.1</oid>
                <filter-type>included</filter-type>
              </config>
            </oid-tree>
          </oid-trees>
        </snmp-view>
      </snmp-views>
    </server>
  </servers>
</snmp>
<qos xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-qos">
  <global>
    <config>
      <enable-qos>enable</enable-qos>
    </config>
  </global>
  <interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-qos-if">
    <interface>
      <name>ce20</name>
      <config>
        <name>ce20</name>
      </config>
    </interface>
    <interface>
      <name>ce21</name>
      <config>
        <name>ce21</name>
      </config>
    </interface>
    <interface>
      <name>ge0</name>
      <config>
        <name>ge0</name>
      </config>
    </interface>
    <interface>
      <name>ge1</name>
      <config>
        <name>ge1</name>
      </config>
    </interface>
    <interface>
      <name>ge2</name>
      <config>
        <name>ge2</name>
      </config>
    </interface>
    <interface>
      <name>ge3</name>
      <config>
        <name>ge3</name>
      </config>
    </interface>
    <interface>
      <name>xe10</name>
      <config>
        <name>xe10</name>
      </config>
    </interface>
    <interface>
      <name>xe11</name>
      <config>
        <name>xe11</name>
      </config>
    </interface>
    <interface>
      <name>xe12</name>
      <config>
        <name>xe12</name>
      </config>
    </interface>
    <interface>
      <name>xe13</name>
      <config>
        <name>xe13</name>
      </config>
    </interface>
    <interface>
      <name>xe14</name>
      <config>
        <name>xe14</name>
      </config>
    </interface>
    <interface>
      <name>xe15</name>
      <config>
        <name>xe15</name>
      </config>
    </interface>
    <interface>
      <name>xe16</name>
      <config>
        <name>xe16</name>
      </config>
    </interface>
    <interface>
      <name>xe17</name>
      <config>
        <name>xe17</name>
      </config>
    </interface>
    <interface>
      <name>xe18</name>
      <config>
        <name>xe18</name>
      </config>
    </interface>
    <interface>
      <name>xe19</name>
      <config>
        <name>xe19</name>
      </config>
    </interface>
    <interface>
      <name>xe4</name>
      <config>
        <name>xe4</name>
      </config>
    </interface>
    <interface>
      <name>xe5</name>
      <config>
        <name>xe5</name>
      </config>
    </interface>
    <interface>
      <name>xe6</name>
      <config>
        <name>xe6</name>
      </config>
    </interface>
    <interface>
      <name>xe7</name>
      <config>
        <name>xe7</name>
      </config>
    </interface>
    <interface>
      <name>xe8</name>
      <config>
        <name>xe8</name>
      </config>
    </interface>
    <interface>
      <name>xe9</name>
      <config>
        <name>xe9</name>
      </config>
    </interface>
  </interfaces>
</qos>
<profiles xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-platform">
  <hardware-profile>
    <statistics>
      <config>
        <ingress-acl></ingress-acl>
      </config>
    </statistics>
  </hardware-profile>
</profiles>
<port-mirror xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-mirror">
  <sessions>
    <session>
      <id>1</id>
      <config>
        <id>1</id>
        <type>local</type>
        <enabled></enabled>
      </config>
      <destination>
        <local>
          <config>
            <interface-name>xe4</interface-name>
          </config>
        </local>
      </destination>
      <source-interfaces>
        <source-interface>
          <name>xe16</name>
          <config>
            <name>xe16</name>
            <direction>rx tx</direction>
          </config>
        </source-interface>
        <source-interface>
          <name>xe6</name>
          <config>
            <name>xe6</name>
            <direction>rx tx</direction>
          </config>
        </source-interface>
      </source-interfaces>
    </session>
    <session>
      <id>2</id>
      <config>
        <id>2</id>
        <type>local</type>
        <enabled></enabled>
      </config>
      <destination>
        <local>
          <config>
            <interface-name>xe5</interface-name>
          </config>
        </local>
      </destination>
      <source-interfaces>
        <source-interface>
          <name>xe15</name>
          <config>
            <name>xe15</name>
            <direction>rx tx</direction>
          </config>
        </source-interface>
        <source-interface>
          <name>xe19</name>
          <config>
            <name>xe19</name>
            <direction>rx tx</direction>
          </config>
        </source-interface>
      </source-interfaces>
    </session>
  </sessions>
</port-mirror>
<ptp xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-ptp">
  <ptp-instances>
    <ptp-instance>
      <instance-type>0</instance-type>
      <config>
        <instance-type>0</instance-type>
        <profile>g8275.1</profile>
      </config>
      <default-data-set>
        <config>
          <clock-type-tgm>tgm</clock-type-tgm>
          <number-ports>21</number-ports>
        </config>
      </default-data-set>
      <ports>
        <port>
          <port-number>1</port-number>
          <config>
            <port-number>1</port-number>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>gps</network-interface>
              <config>
                <network-interface>gps</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>2</port-number>
          <config>
            <port-number>2</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe6</network-interface>
              <config>
                <network-interface>xe6</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>3</port-number>
          <config>
            <port-number>3</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe7</network-interface>
              <config>
                <network-interface>xe7</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>4</port-number>
          <config>
            <port-number>4</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe8</network-interface>
              <config>
                <network-interface>xe8</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>5</port-number>
          <config>
            <port-number>5</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe9</network-interface>
              <config>
                <network-interface>xe9</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>6</port-number>
          <config>
            <port-number>6</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe10</network-interface>
              <config>
                <network-interface>xe10</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>7</port-number>
          <config>
            <port-number>7</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe11</network-interface>
              <config>
                <network-interface>xe11</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>8</port-number>
          <config>
            <port-number>8</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe12</network-interface>
              <config>
                <network-interface>xe12</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>9</port-number>
          <config>
            <port-number>9</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe13</network-interface>
              <config>
                <network-interface>xe13</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>10</port-number>
          <config>
            <port-number>10</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe14</network-interface>
              <config>
                <network-interface>xe14</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>11</port-number>
          <config>
            <port-number>11</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe15</network-interface>
              <config>
                <network-interface>xe15</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>12</port-number>
          <config>
            <port-number>12</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe16</network-interface>
              <config>
                <network-interface>xe16</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>13</port-number>
          <config>
            <port-number>13</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe17</network-interface>
              <config>
                <network-interface>xe17</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>14</port-number>
          <config>
            <port-number>14</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe18</network-interface>
              <config>
                <network-interface>xe18</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>15</port-number>
          <config>
            <port-number>15</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>xe19</network-interface>
              <config>
                <network-interface>xe19</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>16</port-number>
          <config>
            <port-number>16</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>ge0</network-interface>
              <config>
                <network-interface>ge0</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
        <port>
          <port-number>17</port-number>
          <config>
            <port-number>17</port-number>
            <master-only></master-only>
          </config>
          <network-interfaces>
            <network-interface>
              <network-interface>ge2</network-interface>
              <config>
                <network-interface>ge2</network-interface>
              </config>
            </network-interface>
          </network-interfaces>
        </port>
      </ports>
    </ptp-instance>
  </ptp-instances>
</ptp>
<system-host xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-host">
  <config>
    <service-passwd-encryption>false</service-passwd-encryption>
  </config>
</system-host>
 
    <nacm xmlns="urn:ietf:params:xml:ns:yang:ietf-netconf-acm">
      <enable-nacm>false</enable-nacm>
      <read-default>deny</read-default>
      <write-default>deny</write-default>
      <exec-default>deny</exec-default>
      <enable-external-groups>false</enable-external-groups>
      <groups>
        <group>
          <name>PRIV1</name>
          <user-name>admin</user-name>
          <user-name>ocnos</user-name>
        </group>
      </groups>
      <rule-list>
        <name>admin-rules</name>
        <group>PRIV1</group>
        <rule>
          <name>permit-all</name>
          <action>permit</action>
          <comment>Permit everything for PRIV1 group</comment>
        </rule>
      </rule-list>
    </nacm>
  </data>
</rpc-reply>
```
:::

---

### 1.2 Method 2: Use netopeer2

- Start the netopeer2 tool
    
    ```bash
    netopeer2-cli
    ```
    
- Connect to ufispace FHG mplane
    
    ```bash
    connect --host 192.168.8.25 --port 830 --login ocnos
    ```
    
- Get all configuration
    
    ```bash
    get-config --source running
    ```

---



## 2. Shutdown port

### 2.1 Method 1: Use ncclient to control the M-plane

- Create a new file (Use shutdown as example)
    
    ```bash
    vim editNetconf.py
    ```

    ```python
    from ncclient import manager
    smo = manager.connect(host='192.168.8.25', port="830", timeout=5, username="ocnos", password="ocnos", hostkey_verify=False)

    conf = '''
    <config xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0">
    <interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface">
      <interface>
        <name>xe9</name>
        <config>
          <name>xe9</name>
          <shutdown/>
        </config>
      </interface>
    </interfaces>
    </config>
    '''

    # Example of deleting an shutdown
    # conf = '''
    # <config xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0">
    # <interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface">
    #   <interface>
    #     <name>xe9</name>
    #     <config>
    #       <name>xe9</name>
    #       <shutdown operation="delete"/>
    #     </config>
    #   </interface>
    # </interfaces>
    # </config>
    # '''


    print("Configuration to be applied:==========================================")
    result = smo.edit_config(target="candidate", config=conf, default_operation="merge")
    print(result)
    smo.commit()
    ```
    
- Run the python file
    
    ```bash
    python3 editNetconf.py
    ```
- Result
    
```bash
Configuration to be applied:==========================================
<?xml version="1.0" encoding="UTF-8"?>
<rpc-reply xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0"
  message-id="urn:uuid:703630eb-f7fc-4e78-b5d6-9570db949f6d"
  xmlns="urn:ietf:params:xml:ns:netconf:base:1.0">
  <ok/>
</rpc-reply>
```

- Check using get config
```bash
  <interface>
    <name>xe9</name>
    <config>
      <name>xe9</name>
      <enable-switchport></enable-switchport>
      <mtu>9216</mtu>
      <shutdown></shutdown>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2-4</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
```
---

### 2.2 Method 2: Use netopeer2

- Start the netopeer2 tool
    
    ```bash
    netopeer2-cli
    ```
    
- Connect to ufispace FHG mplane
    
    ```bash
    connect --host 192.168.8.25 --port 830 --login ocnos
    ```
    
- Create a file for control
     ```bash
      vim config.xml
     ```
     
    ```bash
    <interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface">
  <interface>
    <name>xe9</name>
    <config>
      <name>xe9</name>
      <shutdown/>
    </config>
  </interface>
</interfaces>
    ```
- Get all configuration
```bash
edit-config --target candidate --config=config.xml
```


## 3. Enable/Disable port
**Disable xe9 (use netopeer2)**:
```bash
> netopeer2-cli
> connect --host 192.168.8.25 --port 830 --login ocnos
> edit-config --target candidate --config=/home/ubuntu/winnie/o1netconf/disable-switchport.xml
> commit
```

```xml
<interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface"
           xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0">
  <interface>
    <name>xe9</name>
    <config>
      <name>xe9</name>
      <enable-switchport nc:operation="delete"/>
    </config>
  </interface>
</interfaces>
```
- **result**:
```bash=
OcNOS#show running-config interface xe9
!
interface xe9
 synce
  mode synchronous
  output-source
!
```

**Enable xe9 (use netopeer2)**:


```bash
> netopeer2-cli
> connect --host 192.168.8.25 --port 830 --login ocnos
> edit-config --target candidate --config=/home/ubuntu/winnie/o1netconf/enable-switchport.xml
> commit
```


```xml
<interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface">
  <interface>
    <name>xe9</name>
    <config>
      <name>xe9</name>
      <enable-switchport/>
    </config>
  </interface>
</interfaces>
```
- **result**:
```bash=
OcNOS#show running-config interface xe9
!
interface xe9
 switchport
 bridge-group 1
 switchport mode trunk
 switchport trunk allowed vlan add 2-4
 mtu 9216
 synce
  mode synchronous
  output-source
!
```

## 4. Setting bridge-group
```bash
> netopeer2-cli
> connect --host 192.168.8.25 --port 830 --login ocnos
> edit-config --target candidate --config=/home/ubuntu/winnie/o1netconf/bridge-group.xml
> commit
```

```xml
<network-instances xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-network-instance">
  <network-instance>
    <instance-name>1</instance-name>
    <instance-type>l2ni</instance-type>
    <bridge xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-bridge">
      <bridge-ports>
        <interface>
          <name>xe9</name>
          <mstp-port xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-xstp">
            <port-bridge>
              <config>
                <path-cost xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0" nc:operation="delete">1</path-cost>
              </config>
            </port-bridge>
          </mstp-port>
        </interface>
      </bridge-ports>
    </bridge>
  </network-instance>
</network-instances>
```

- **result**:
```bash=
OcNOS#show running-config interface xe9
!
interface xe9
 switchport
 bridge-group 1
 synce
  mode synchronous
  output-source
!
```

## 5. Setting switch mode trunk
```bash
> netopeer2-cli
> connect --host 192.168.8.25 --port 830 --login ocnos
> edit-config --target candidate --config=/home/ubuntu/winnie/o1netconf/trunk.xml
> commit
```

```xml
<interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface">
  <interface>
    <name>xe9</name>
    <config>
      <name>xe9</name>
    </config>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
</interfaces>
```

- **result**:
```bash=
OcNOS#show running-config interface xe9
!
interface xe9
 switchport
 bridge-group 1
 switchport mode trunk
 synce
  mode synchronous
  output-source
!
```
![image](https://hackmd.io/_uploads/H1mSSOM2ee.png)


## 5. Add vlan
```bash
> netopeer2-cli
> connect --host 192.168.8.25 --port 830 --login ocnos
> edit-config --target candidate --config=/home/ubuntu/winnie/o1netconf/setting_vlan.xml
> commit
```

```xml
<interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface"
            xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0">
  <interface>
    <name>xe9</name>
    <port-vlan xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-port-vlan">
      <switched-vlans>
        <switched-vlan>
          <interface-mode>trunk</interface-mode>
          <config>
            <interface-mode>trunk</interface-mode>
          </config>
          <allowed-vlan>
            <config>
              <allowed-vlan-id>2,4-7</allowed-vlan-id>
            </config>
          </allowed-vlan>
        </switched-vlan>
      </switched-vlans>
    </port-vlan>
  </interface>
</interfaces>

```

- **result**:
```bash=
OcNOS#show running-config interface xe9
!
interface xe9
 switchport
 bridge-group 1
 switchport mode trunk
 switchport trunk allowed vlan add 2,4-7
 synce
  mode synchronous
  output-source
!
```


## 6.Setting mtu
```bash
> netopeer2-cli
> connect --host 192.168.8.25 --port 830 --login ocnos
> edit-config --target candidate --config=/home/ubuntu/winnie/o1netconf/mtu.xml
> commit
```

```xml
<interfaces xmlns="http://www.ipinfusion.com/yang/ocnos/ipi-interface"
            xmlns:nc="urn:ietf:params:xml:ns:netconf:base:1.0">
  <interface>
    <name>xe9</name>
    <config>
      <name>xe9</name>
      <mtu>9216</mtu>
    </config>
  </interface>
</interfaces>
```

- **result**:
```bash=
OcNOS#show running-config interface xe9
!
interface xe9
 switchport
 bridge-group 1
 switchport mode trunk
 switchport trunk allowed vlan add 2,4-7
 mtu 9216
 synce
  mode synchronous
  output-source
!
```

## 7. Current staus for xe9
```bash=
ssh ocnos@192.168.8.25
ocnos@192.168.8.25's password: 
Linux OcNOS 6.1.76-g1ae9a6ccd #1 SMP PREEMPT_DYNAMIC Thu Jun 26 12:50:38 UTC 2025 x86_64
Last login: Thu Sep 25 08:05:11 2025 from 192.168.8.115

OcNOS version UFI_S9500-22XST-OcNOS-6.6.1.140-CSR_Q1-MR  07/01/2025 14:44:10
OcNOS>enable
OcNOS#show running-config interface xe9
!
interface xe9
 switchport
 bridge-group 1
 switchport mode trunk
 switchport trunk allowed vlan add 2,4-7
 mtu 9216
 synce
  mode synchronous
  output-source
!
```
![image](https://hackmd.io/_uploads/HyKjAFm2xl.png)

