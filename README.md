snmpjs-new provides a toolkit for SNMP agents and management applications in
Node.js.

Note: this was forked from http://joyent.github.com/node-snmpjs
for the purpose of various bug fixes.

## Usage

For full docs, see <http://joyent.github.com/node-snmpjs/> (I haven't made a doc page custom to this package).

	var os = require('os');
	var snmp = require('snmpjs');

	var agent = snmp.createAgent();

	agent.request({ oid: '.1.3.6.1.2.1.1.5', handler: function (prq) {
		var nodename = os.hostname();
		var val = snmp.data.createData({ type: 'OctetString',
		    value: nodename });

		snmp.provider.readOnlyScalar(prq, val);
	} });

	agent.bind({ family: 'udp4', port: 161 });

Try hitting that with your favourite SNMP get utility, such as:

	$ snmpget -v 2c -c any localhost .1.3.6.1.2.1.1.5.0

## Installation

	$ npm install snmpjs

## License

MIT.

## Bugs

See <https://github.com/dtgriscom/node-snmpjs-new/issues>.
